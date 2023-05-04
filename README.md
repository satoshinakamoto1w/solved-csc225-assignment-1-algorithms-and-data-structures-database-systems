Download Link: https://assignmentchef.com/product/solved-csc225-assignment-1-algorithms-and-data-structures-database-systems
<br>
<h1></h1>

This programming assignment covers an application of algorithms and data structures arising in the implementation of database systems. Databases and data management are covered by later courses, such as CSC 370. In this assignment, you will design and implement an efficient and correct algorithm for <strong>aggregation</strong>, which is a fundamental operation in relational database systems. Since this is not a database course, the algorithm will operate on simple text-based spreadsheet files instead of a database.

The specification for this assignment can be found in Section 2. Sections 1.1 – 1.3 contain a description and several examples of grouping and aggregation, using the following (fictional) table of student numbers and grades.

<table width="323">

 <tbody>

  <tr>

   <td width="80"></td>

   <td colspan="2" width="193">Table grades</td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="80"><strong>id</strong></td>

   <td width="105"><strong>course subject</strong></td>

   <td width="88"><strong>course num</strong></td>

   <td width="51"><strong>grade</strong></td>

  </tr>

  <tr>

   <td width="80">V00123457</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">78</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="51">63</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">75</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">85</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">72</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="51">68</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">70</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">79</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">47</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">91</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">68</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">89</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">40</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="51">74</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="51">71</td>

  </tr>

 </tbody>

</table>

<h2>1.1        Counts and Averages by Student</h2>

Consider the task of computing the number of courses taken by each student, or the task of computing the average grade for each student. For both of these tasks, the rows of the table need to be divided into groups by student number (which is the id column of the table). Then, the number of courses per student or average grade per student can be computed by counting or averaging the grade values within each group. Applying a function (such as counting or averaging) to collapse a group of rows into a single row is called <strong>aggregation</strong>. The table on the left below shows the groupings of rows by the id column, with each group receiving a different colour, and the tables on the right show the counts and averages within each group. Notice that the only columns in the result tables are the grouping criteria (in this case, the id column) and the aggregation result. All other columns in the original table are omitted.

<table width="323">

 <tbody>

  <tr>

   <td colspan="4" width="323">Table grades</td>

  </tr>

  <tr>

   <td width="80"><strong>id</strong></td>

   <td width="105"><strong>course subject</strong></td>

   <td width="88"><strong>course num</strong></td>

   <td width="51"><strong>grade</strong></td>

  </tr>

  <tr>

   <td width="80">V00123457</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">78</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="51">63</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">75</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">85</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">72</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="51">68</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">70</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">79</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">47</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">91</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">68</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">89</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">40</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="51">74</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="51">71</td>

  </tr>

 </tbody>

</table>

<table width="207">

 <tbody>

  <tr>

   <td colspan="2" width="207">Aggregation (Counting Rows)</td>

  </tr>

  <tr>

   <td width="80"><strong>id</strong></td>

   <td width="127"><strong>count(grade)</strong></td>

  </tr>

  <tr>

   <td width="80">V00123457</td>

   <td width="127">1</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="127">5</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="127">3</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="127">3</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="127">3</td>

  </tr>

 </tbody>

</table>

<table width="174">

 <tbody>

  <tr>

   <td colspan="2" width="174">Aggregation (Averaging)</td>

  </tr>

  <tr>

   <td width="80"><strong>id</strong></td>

   <td width="94"><strong>avg(grade)</strong></td>

  </tr>

  <tr>

   <td width="80">V00123457</td>

   <td width="94">78</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="94">74</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="94">68.66</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="94">60</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="94">78.66</td>

  </tr>

 </tbody>

</table>

Result of aggregation by counting the number of grade values in each group.

Original table, grouped by <sub>id </sub>column.            Result of aggregation by averaging the grade values in each group.

<h2>1.2        Averages by Subject</h2>

Consider the task of computing the average grade within each subject (CSC and MATH). In this case, the grouping criteria is the course_subject column and the aggregation result is avg(grade). The tables below show the grouping and aggregation. As above, notice that the other columns are excluded from the result table.

<table width="323">

 <tbody>

  <tr>

   <td colspan="4" width="323">Table grades</td>

  </tr>

  <tr>

   <td width="80"><strong>id</strong></td>

   <td width="105"><strong>course subject</strong></td>

   <td width="88"><strong>course num</strong></td>

   <td width="51"><strong>grade</strong></td>

  </tr>

  <tr>

   <td width="80">V00123457</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">78</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="51">63</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">75</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">85</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">72</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="51">68</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">70</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">79</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">47</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">91</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">68</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">89</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">40</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="51">74</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="51">71</td>

  </tr>

 </tbody>

</table>

<table width="188">

 <tbody>

  <tr>

   <td colspan="2" width="188">Aggregation Result</td>

  </tr>

  <tr>

   <td width="105"><strong>course </strong><strong>subject</strong></td>

   <td width="83"><strong>avg(grade)</strong></td>

  </tr>

  <tr>

   <td width="105">CSC</td>

   <td width="83">72.18</td>

  </tr>

  <tr>

   <td width="105">MATH</td>

   <td width="83">69</td>

  </tr>

 </tbody>

</table>

Result of aggregation by averaging the grade values in each group.

Original table, grouped by the course_subject column.

<h2>1.3        Averages by Course</h2>

Now suppose we want to compute the average grade for each course. It is not sufficient to group by the course_num column, since two courses with the same number may not be the same course (for example, consider CSC 110 and MATH 110). The grouping criteria therefore must include two columns: course_subject and course_num. The tables below show the grouping and aggregation. Again, the only columns in the output table are the grouping criteria and the aggregation result.

<table width="323">

 <tbody>

  <tr>

   <td colspan="4" width="323">Table grades</td>

  </tr>

  <tr>

   <td width="80"><strong>id</strong></td>

   <td width="105"><strong>course subject</strong></td>

   <td width="88"><strong>course num</strong></td>

   <td width="51"><strong>grade</strong></td>

  </tr>

  <tr>

   <td width="80">V00123457</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">78</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="51">63</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">75</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">85</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">72</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="51">68</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">70</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">79</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="51">47</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">91</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="51">68</td>

  </tr>

  <tr>

   <td width="80">V00123456</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">89</td>

  </tr>

  <tr>

   <td width="80">V00951413</td>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="51">40</td>

  </tr>

  <tr>

   <td width="80">V00314159</td>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="51">74</td>

  </tr>

  <tr>

   <td width="80">V00654322</td>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="51">71</td>

  </tr>

 </tbody>

</table>

<table width="276">

 <tbody>

  <tr>

   <td colspan="3" width="276">Aggregation Result</td>

  </tr>

  <tr>

   <td width="105"><strong>course subject</strong></td>

   <td width="88"><strong>course num</strong></td>

   <td width="83"><strong>avg(grade)</strong></td>

  </tr>

  <tr>

   <td width="105">CSC</td>

   <td width="88">225</td>

   <td width="83">74.5</td>

  </tr>

  <tr>

   <td width="105">MATH</td>

   <td width="88">110</td>

   <td width="83">65.5</td>

  </tr>

  <tr>

   <td width="105">CSC</td>

   <td width="88">110</td>

   <td width="83">67</td>

  </tr>

  <tr>

   <td width="105">CSC</td>

   <td width="88">106</td>

   <td width="83">73.75</td>

  </tr>

  <tr>

   <td width="105">MATH</td>

   <td width="88">100</td>

   <td width="83">72.5</td>

  </tr>

 </tbody>

</table>

Result of aggregation by averaging the grade values in each group.

Original table, grouped by the course_subject and course_num columns.

<h1>2              Specification</h1>

Your task for this assignment is to write a Java program Aggregate which reads a table from a text file and performs grouping and aggregation with one of three aggregation functions: count (count the number of rows in each group), sum (add up all elements in the aggregation column within each group) and avg (compute the average of all elements in the aggregation column within each group). To receive full marks, the entire implementation must be correct, allow any number of columns to be used as grouping criteria, and run in <em>O</em>(<em>n</em>log<sub>2</sub><em>n</em>) time on a table with <em>n </em>rows. See Section 3 for more details on the evaluation process.

<h2>2.1        Data Format</h2>

Tabular data can be stored in a variety of ways. One simple format for text-based tables and spreadsheets is the comma-separated value (CSV) format. Files in CSV format normally have the extension .csv or .txt. A CSV spreadsheet consists of a line of text for each row of data, with each column separated by a comma. In this assignment, column headings will be given as the first row of the spreadsheet, and no comma will appear after the last column on each line.

The grades table in Section 1 would be represented in CSV format as follows.

id,course_subject,course_num,grade V00123457,CSC,225,78

V00654322,MATH,110,63

V00654322,CSC,110,75

V00314159,CSC,106,85

V00951413,CSC,106,72

V00951413,MATH,110,68

V00654322,CSC,106,70

V00123456,CSC,110,79

V00314159,CSC,110,47

V00654322,CSC,225,91

V00123456,CSC,106,68

V00123456,CSC,225,89

V00951413,CSC,225,40

V00314159,MATH,100,74

V00654322,MATH,100,71

Formally, the CSV files used in this assignment will conform to the following specification. • Every CSV file must contain at least one non-blank line, which will contain the column headings.

<ul>

 <li>Blank lines (consisting entirely of whitespace characters such as spaces and tabs) will be completely ignored (and will not count as a row of the table).</li>

 <li>You may assume that every line contains the same number of columns (an input file with an inconsistent number of columns per line will be considered invalid).</li>

 <li>There is no limit to the number of columns (as long as every line has the same number of columns) or the number of rows in the file.</li>

 <li>The data in the file may contain letters, numbers, spaces and punctuation, with one exception:</li>

</ul>

comma characters will only appear as column separators (they may not appear in the data). • The number of columns is equal to the number of commas in the line plus one. The data in a column may be blank. For example, the line ‘Hello,,World,’ contains four columns. The second and fourth columns are blank.

<h2>2.2        Aggregate program interface</h2>

Your Aggregate program will accept command line arguments in the form

$ java Aggregate &lt;function&gt; &lt;aggregation column&gt; &lt;input file&gt; &lt;group column 1&gt; &lt;group column 2&gt; … where

<ul>

 <li>&lt;function&gt; is one of ‘count’, ‘sum’ or ‘avg’,</li>

 <li>&lt;aggregation column&gt; is the column name of the column to aggregate,</li>

 <li>&lt;input file&gt; is the name of the input CSV file, and</li>

 <li>the &lt;group column x&gt; arguments are column names of grouping columns (at least one must be specified, but in a complete implementation, any number of grouping columns should be allowed).</li>

</ul>

For example, if the table from Section 1 is contained in the file table_of_grades.csv, the number of grades per student (from Section 1.1) would be computed with the command

$ java Aggregate count grade table_of_grades.csv id and the average grade in each course (from Section 1.3) would be computed with the command

$ java Aggregate avg grade table_of_grades.csv course_subject course_num The program will report an error if any of the following conditions arise.

<ul>

 <li>The &lt;function&gt; argument is not one of ‘count’, ‘sum’ or ‘avg’.</li>

 <li>The input file does not exist, cannot be opened or is not in the correct format.</li>

 <li>The aggregation column or any of the grouping columns do not exist in the input file.</li>

 <li>The aggregation column contains any non-numerical data (except the column header). Other columns may contain non-numerical data.</li>

 <li>A column is used as both a grouping column and an aggregation column.</li>

</ul>

If none of the above errors occur, the program will perform the aggregation and output the resulting table to standard output (that is, the console) in the CSV format described in the previous section, including column headers. The <strong>only </strong>columns that will appear in the output table are the grouping columns and the aggregation result. The grouping columns must appear first, with the last column containing the aggregation result. The column name of the aggregation result column should contain the function name (count, sum or avg) and the name of the original column (e.g. count(grade) or avg(temperature)). The rows of the result table may appear in any order, as long as the header row is first (so you do not have to ensure that the order matches the examples in this document). For example, with table_of_grades.csv defined as in the examples above, the output of the command

$ java Aggregate avg grade table_of_grades.csv course_subject course_num would be course_subject,course_num,avg(grade) CSC,106,73.75

CSC,110,67.0

CSC,225,74.5

MATH,100,72.5

MATH,110,65.5

<h2>2.3        Using Outside Code</h2>

You are encouraged to use the features of the Java Standard Library (including any of the data structures it provides) in your code. If you use a standard library data structure, make sure you are aware of the running times of the operations you use, since that will be important for determining the running time of your program.

There should be no need to use large volumes of code from other sources (such as outside libraries or the internet) in this assignment. If you believe that your implementation requires an outside library, talk to your instructor.

If you find a small snippet of code on the internet that you want to use (for example, in a StackOverflow thread), put a comment in your code indicating the source (including a complete URL). Remember that using code from an outside source without citation is plagiarism.

You are encouraged to discuss the assignment with your peers, and even to share implementation advice or algorithm ideas. However, you are not permitted to use any code from another CSC 225 student under any circumstances, nor are you permitted to share your code in any way with any other student (or the internet) until after the marking is complete. Sharing your code with others before marking is completed, or using another student’s code for assistance (even if you do not directly copy it) is plagiarism.

<h2>2.4        Implementation Advice</h2>

Although this assignment may seem daunting, most of the complexity lies in the specification (since this application is likely new to you) and in the finishing touches needed to make the algorithm asymptotically fast. The actual volume of code needed may be significantly less than assignments you have completed in the past. Your instructor’s solution required about 150 lines of Java code.

You are encouraged to try designing a solution from scratch, since the design process is often the most difficult part of a software project. However, if you are stuck, or feeling uninspired, consider implementing your solution in the following steps.

<ol>

 <li>Write a simple program to read a CSV file into an array or list, then output the data in CSV format. Test this thoroughly to ensure that it is correct. To make things easier later, use separate methods for the input and output code. You may use outside libraries to read/write CSV data, but it is likely easier to write this component yourself.</li>

 <li>Write a method which takes a table and a set of column names as input, then produces a new table containing only the provided columns (for example, given the grades table used in previous examples and the column names ‘id’ and ‘grade’, the method would make a new table containing only the ‘id’ and ‘grade’ columns). Once this feature has been written, verify that your code can read an input file and prune away all columns besides the group columns and aggregation column, then print the resulting table (without any aggregation being performed). Note that you will receive some marks if you can reach this point (see Section 3).</li>

 <li>Write a simple (but possibly slow) aggregation algorithm and verify that it works. Various algorithm ideas will be covered in lectures and labs. It is far more important to have working code than fast code (if your code is not correct, you will receive no marks for its performance).</li>

 <li>Once you have a working implementation (even if it is slow), make sure you can analyse and explain its running time. Add comments and other documentation if necessary to clarify complicated parts of the code. Hand in your working implementation.</li>

 <li>If your code does not have a worst case running time of <em>O</em>(<em>n</em>log<sub>2</sub><em>n</em>), try implementing an improved algorithm. Again, it is better to submit a slow but correct implementation than a fast but incorrect one. Additionally, a fast implementation will not receive full marks unless you can justify its running time.</li>

</ol>

<strong>Note</strong>: You should not use a hash table (or any hashing-based Java data structures, like HashMap) for your implementation if you want your code to have a <strong>worst case </strong><em>O</em>(<em>n</em>log<sub>2</sub><em>n</em>) running time. Although hash tables are very useful in most cases, they have a relatively poor worst-case running time. We will study hash tables in June.