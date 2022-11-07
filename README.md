# Exercise-2
a) Algorithm
Convert the entered numbers to Ordinal form(in words)
1) Create a function ConvertToWord with pararmeters number and output
2) Inside the function create an if statement such that if the number is '0' the result will be "zeroth"
3) Create 4 arrays such that: 
   Array1 contains all numbers from 1 to 9 in words 
   Array2 contains all numbers multiple of 10  from 10 to 90 in words 
   Array3 contains all numbers from 1 to 9 in ordinal 
   Array4 contains all numbers multiple of 10 from 10 to 90 in ordinal
4) Check if the number is divisible by 10 the digit is in one's place
5) Check if statement such that if the digit is in hundreds place output the digit from array1 and array2 followed by the word hundred,thousand and million
6) Check if the digit is in tens places and the digit in one's place is zero 
7) Output the corressponding value from array3
    Else check if the digit in one's place is non zero and the digit at ten's place is a non zero
    Output the coressponding value from array2 and array4
8) Return output 
9) Take the input number from the user and call the function
10) Print the entered number and the output



b) Code
<?php
function ConvertToWord($num) {
    if (empty($num[0])) 
    {
       $output = "zeroth";
    }
     $ord = array(1=> "first", 2 => "second", 3 => "third", 4 => "fourth", 5 => "fifth", 6 => "sixth", 7 => "seventh", 8 => "eighth", 9 => "ninth", 10 => "tenth", 11 => " eleventh", 12 => " twelfth", 13 => " thirteenth", 14 => " fourteenth", 15 => " fifteenth", 16 => " sixteenth", 17 => " seventeenth", 18 => " eighteenth", 19 => " nineteenth");
     $num_single = array("zero","one", "two", "three", "four", "five", "six", "seven", "eight", " nine", " ten", "eleven", " twelve", " thirteen", " fourteen", "fifteen", " sixteen", " seventeen", " eighteen", " nineteen");
     $num_double = array(""," ten", " twenty", " thirty", " forty", " fifty", " sixty", " seventy", " eighty", " ninety");
     $places = array(2 => "hundred","thousand", 6 => "million", 9 => "billion", 12 => "trillion");

     $num= array_reverse(str_split($num));
  if ($num[0]== 0) {
        if ($num[1] >= 2)
            $output = str_replace("y", "ieth", $num_double[$num[1]]);
        else
            $output = $num_double[$num[1]]."th";
    } 
    else if ($num[1] == 1) {
        $output = $ord[$num[1] . $num[0]];
    } 
    else {	
        if (array_key_exists($num[0], $ord))
            $output = $ord[$num[0]];
        else
            $output = $num_single[$num[0]]."th";
    }
        
    if($num[0] == 0 || $num[1] == 1){
        $i = 2;
    } else {
        $i = 1;
    }
    
    while ($i < count($num)) {
        if ($i == 1) {
            $output = $num_double[$num[$i]] . " " . $output;
            $i++;
        } else if ($i == 2) {
            $output = $num_single[$num[$i]] . " hundred" . $output;	
            $i++;
        } else {
            if (isset($num[$i + 2])) {
                $temp = $num_single[$num[$i + 2]] . " hundred ";
                $tempnum = $num[$i + 1].$num[$i];
                if ($tempnum < 20)
                    $temp .= $num_single[$tempnum] . " " . $places[$i] . " ";
                else 
                    $temp .= $num_double[$num[$i + 1]] . " " . $num_single[$num[$i]] . " " . $places[$i] . " ";
                
                $output = $temp . $output;
                $i+=3;
            } else if (isset($num[$i + 1])) {
                $tempnum = $num[$i + 1].$num[$i];
                if ($tempnum < 20)
                    $output = $num_single[$tempnum] . " " . $places[$i] . " " . $output;
                else 
                    $output = $num_double[$num[$i + 1]] . " " . $num_single[$num[$i]] . " " . $places[$i] . " " . $output;
                $i+=2;
            } else {
                $output = $num_single[$num[$i]] . " " . $places[$i] . " " . $output;
                $i++;
            }
        }
    }
 if (empty($num)) 
    {
        $output = "zeroth";
    }
    return $output;
}
$num= (int)readline('Enter a number: ');
echo  ("Entered number is ".$num) ;
echo "   ";
 echo ConvertToWord($num)
 ?> 
