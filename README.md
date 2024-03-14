# coderbytecode

# 1 - Have the function MatchingCharacters(str) take the str parameter being passed and determine the largest number of unique characters that exists between a pair of matching letters anywhere in the string. For example: if str is "ahyjakh" then there are only two pairs of matching letters, the two a's and the two h's. Between the pair of a's there are 3 unique characters: h, y, and j. Between the h's there are 4 unique characters: y, j, a, and k. So for this example your program should return 4. Another example: if str is "ghececgkaem" then your program should return 5 because the most unique characters exists within the farthest pair of e characters. The input string may not contain any character pairs, and in that case your program should just return 0. The input will only consist of lowercase alphabetic characters. */

# Ans ->
function StringChallenge(str) { 

  var maxUnique=0

  for(var i=0;i<str.length;i++)
  {
      for(var j=i+1;j<str.length;j++)
   {
     if(str[i]===str[j])
     {
       var uniqueChars=countUniqueChars(str.substring(i+1,j));
       if(uniqueChars>maxUnique)
       {
         maxUnique=uniqueChars;
       }
     }
   }
   }
   return maxUnique;
}
  function countUniqueChars(substring)
  {
    var charSet={};
    for(var i=0;i<substring.length;i++)
    {
      charSet[substring[i]]=true;}
      return Object.keys(charSet).length;}
    
  StringChallenge('ghececgkaem')

console.log(StringChallenge(readline()));



2. Front-end Challenge

We provided some simple JavaScript template code. Your goal is to modify the application so that you can properly toggle the button to switch between an ON state and an OFF state. When the button is on and it is clicked, it turns off and the text within it changes from ON to OFF and vice versa. Only replace the text within the DOM element, do not replace the entire DOM element. You are free to add classes and styles, but make sure you leave the element ID's as they are.


ans ->
const rootApp = document.getElementById("root");
rootApp.innerHTML = '<button id="toggleButton">ON</button>';

// Add event listener to the button
document.getElementById("toggleButton").addEventListener("click", function() {
    const button = document.getElementById("toggleButton");
    // Toggle the text content between "ON" and "OFF"
    button.textContent = button.textContent === "ON" ? "OFF" : "ON";
});

3. Searching Challenge

Have the function

SearchingChallenge (strArr) take the array of strings stored in strazz, which will be a 2D matrix of 0 and 1's, and determine how many holes, or contiguous regions of 0's, exist in the matrix. A contiguous region is one where there is a connected group of 0's going in one or more of four directions: up, down, left, or right. For example: if strArr is ["10111", "10101", "11101", "11111"], then this looks like the following matrix:

10111

10101

11101

For the input above, your program should return 2 because there are two separate contiguous regions of 0's, which create "holes" in the matrix. You can assume the input will not be empty.

Examples

Type there to search For the input above, your program should return 2 because there are two separate contiguous regions of 0's, which create "holes" in the matrix. You can assume the input will not be empty.

Examples

Input: ["01111", "01101", "00011", "11110"]

Output: 3

Input: ["1011", "0010"]

Output: 2


ans ->
function BitmapHoles(strArr) {
    const matrix = strArr.map(row => row.split(''));

    function dfs(row, col) {
        console.log('Exploring:', row, col); // Log current position

        if (row < 0 || row >= matrix.length || col < 0 || col >= matrix[0].length || matrix[row][col] === '1') {
            console.log('Out of bounds or visited:', row, col); // Log if out of bounds or visited
            return;
        }

        matrix[row][col] = '1'; // Mark as visited

        // Explore neighbors in four directions
        dfs(row - 1, col); // Up
        dfs(row + 1, col); // Down
        dfs(row, col - 1); // Left
        dfs(row, col + 1); // Right
    }

    let holeCount = 0;

    for (let i = 0; i < matrix.length; i++) {
        for (let j = 0; j < matrix[0].length; j++) {
            if (matrix[i][j] === '0') {
                console.log('Starting DFS at:', i, j); // Log starting position of DFS
                holeCount++;
                dfs(i, j);
            }
        }
    }

    return holeCount;
}

// Test cases
console.log(BitmapHoles(["10111", "10101", "11101", "11111"])); // Output: 2
console.log(BitmapHoles(["01111", "01101", "00011", "11110"])); // Output: 3
console.log(BitmapHoles(["1011", "0010"])); // Output: 2


4. Have the function TreeConstructor(strArr) take the array of strings stored in strArr, which will contain pairs of integers in the following format: (i1,i2), where i1 represents a child node in a tree and the second integer i2 signifies that it is the parent of i1. For example: if strArr is ["(1,2)", "(2,4)", "(7,2)"], then this forms the following tree: which you can see forms a proper binary tree. Your program should, in this case, return the string true because a valid binary tree can be formed. If a proper binary tree cannot be formed with the integer pairs, then return the string false. All of the integers within the tree will be unique, which means there can only be one node in the tree with the given integer value. Examples Input: ["(1,2)", "(2,4)", "(5,7)", "(7,2)", "(9,5)"] Output: true Input: ["(1,2)", "(3,2)", "(2,12)", "(5,2)"] Output: false


  function TreeConstructor(strArr) { 
  var arr = [];
  var counts = {};
  
  for (var i = 0; i < strArr.length; i++) {
    var pair = strArr[i].match(/\d+/g);
    arr.push(pair[0]);
    arr.push(pair[1]);
  }
  
  arr.forEach(function(x) {
    counts[x] = (counts[x] || 0) + 1;
  });
  
  for (var j in counts) {
    if (counts[j] >= 4) {
      return false;
    }
  }
  
  return true;
}


5. Back-end Challenge

In the PHP file, write a program to perform a GET request on the route

https://coderbyte.com/api/challenge s/json/age-counting which contains a data key and the value is a string which contains items in the format: key=STRING, age=INTEGER. Your goal is to count how many items exist that have an age equal to or greater than 50, and print this final value.

Example Input

{"data":"key=IAfpK, age=58, key=WNVdi, age=64, key=jp9zt, age=47"}

Example Output

2


ans ->
<?php
$ch = curl_init('https://coderbyte.com/api/challenges/json/age-counting');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HEADER, 0);
$data = curl_exec($ch);
curl_close($ch);

$json_data = json_decode($data, true);
$items = explode(', ', $json_data['data']);
$count = array_reduce($items, function ($count, $item) {
  if (strpos($item, 'age=') !== false) {
    $age = explode('=', $item)[1];
    if ($age >= 50) return $count + 1;
  }
  return $count;
}, 0);

print_r($count);
