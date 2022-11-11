# Exercise-2
a) Algorithm<br>
Convert the entered numbers to Ordinal form(in words)<br>
1) Create a function ConvertToWord with pararmeters number and output<br>
2) Inside the function create an if statement such that if the number is '0' the result will be "zeroth"<br>
3) Create 4 arrays such that:<br>
   Array1 contains all numbers from 1 to 9 in words<br> 
   Array2 contains all numbers multiple of 10  from 10 to 90 in words<br> 
   Array3 contains all numbers from 1 to 9 in ordinal <br>
   Array4 contains all numbers multiple of 10 from 10 to 90 in ordinal<br>
4) Check if the number is divisible by 10 the digit is in one's place<br>
5) Check if statement such that if the digit is in hundreds place output the digit from array1 and array2 followed by the word hundred,thousand and million<br>
6) Check if the digit is in tens places and the digit in one's place is zero <br>
7) Output the corressponding value from array3<br>
    Else check if the digit in one's place is non zero and the digit at ten's place is a non zero<br>
    Output the coressponding value from array2 and array4<br>
8) Return output <br>
9) Take the input number from the user and call the function<br>
10) Print the entered number and the output<br>



b) Code<br>
       <?php<br>
   function ConvertToWord($num) {<br>
    if (empty($num[0])) <br>
    {<br>
       $output = "zeroth";<br>
    }<br>
     $ord = array(1=> "first", 2 => "second", 3 => "third", 4 => "fourth", 5 => "fifth", 6 => "sixth", 7 => "seventh", 8 => "eighth", 9 => "ninth", 10 => "tenth", 11 => " eleventh", 12 => " twelfth", 13 => " thirteenth", 14 => " fourteenth", 15 => " fifteenth", 16 => " sixteenth", 17 => " seventeenth", 18 => " eighteenth", 19 => " nineteenth");<br>
     $num_single = array("zero","one", "two", "three", "four", "five", "six", "seven", "eight", " nine", " ten", "eleven", " twelve", " thirteen", " fourteen", "fifteen", " sixteen", " seventeen", " eighteen", " nineteen");<br>
     $num_double = array(""," ten", " twenty", " thirty", " forty", " fifty", " sixty", " seventy", " eighty", " ninety");<br>
     $places = array(2 => "hundred","thousand", 6 => "million", 9 => "billion", 12 => "trillion");<br>
     $num= array_reverse(str_split($num));<br>
  if ($num[0]== 0) {<br>
        if ($num[1] >= 2)<br>
            $output = str_replace("y", "ieth", $num_double[$num[1]]);<br>
        else<br>
            $output = $num_double[$num[1]]."th";<br>
    } <br>
    else if ($num[1] == 1) {<br>
        $output = $ord[$num[1] . $num[0]];<br>
    } <br>
    else {<br>	
        if (array_key_exists($num[0], $ord))<br>
            $output = $ord[$num[0]];<br>
        else<br>
            $output = $num_single[$num[0]]."th";<br>
    }<br>
    if($num[0] == 0 || $num[1] == 1){<br>
        $i = 2;<br>
    } else {<br>
        $i = 1;<br>
    }<br>
    while ($i < count($num)) {<br>
        if ($i == 1) {<br>
            $output = $num_double[$num[$i]] . " " . $output;<br>
            $i++;<br>
        } else if ($i == 2) {<br>
            $output = $num_single[$num[$i]] . " hundred" . $output;<br>	
            $i++;<br>
        } else {<br>
            if (isset($num[$i + 2])) {<br>
                $temp = $num_single[$num[$i + 2]] . " hundred ";<br>
                $tempnum = $num[$i + 1].$num[$i];<br>
                if ($tempnum < 20)<br>
                    $temp .= $num_single[$tempnum] . " " . $places[$i] . " ";<br>
                else <br>
                    $temp .= $num_double[$num[$i + 1]] . " " . $num_single[$num[$i]] . " " . $places[$i] . " ";<br>
                
                $output = $temp . $output;<br>
                $i+=3;<br>
            }<br>
                else if (isset($num[$i + 1])) {<br>
                $tempnum = $num[$i + 1].$num[$i];<br>
                if ($tempnum < 20)<br>
                    $output = $num_single[$tempnum] . " " . $places[$i] . " " . $output;<br>
                else <br>
                    $output = $num_double[$num[$i + 1]] . " " . $num_single[$num[$i]] . " " . $places[$i] . " " . $output;<br>
                $i+=2;<br>
            }<br>
                else {<br>
                $output = $num_single[$num[$i]] . " " . $places[$i] . " " . $output;<br>
                $i++;<br>
            }<br>
        }<br>
    }<br>
 if (empty($num))<br> 
    {<br>
        $output = "zeroth";<br>
    }<br>
    return $output;<br>
}<br>
$num= (int)readline('Enter a number: ');<br>
echo  ("Entered number is ".$num) ;<br>
echo "   ";<br>
 echo ConvertToWord($num)<br>
 ?> <br>
