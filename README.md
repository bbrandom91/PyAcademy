

```python
#import pandas and read in the two CSV files
import pandas as pd

file_1 = "raw_data/schools_complete.csv"
file_2 = "raw_data/students_complete.csv"

schools_df = pd.read_csv(file_1)
students_df = pd.read_csv(file_2)
```


```python
#Check out schools file
schools_df.sort_values(by = ['size'])
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>School ID</th>
<th>name</th>
<th>type</th>
<th>size</th>
<th>budget</th>
</tr>
</thead>
<tbody>
<tr>
<th>8</th>
<td>8</td>
<td>Holden High School</td>
<td>Charter</td>
<td>427</td>
<td>248087</td>
</tr>
<tr>
<th>9</th>
<td>9</td>
<td>Pena High School</td>
<td>Charter</td>
<td>962</td>
<td>585858</td>
</tr>
<tr>
<th>4</th>
<td>4</td>
<td>Griffin High School</td>
<td>Charter</td>
<td>1468</td>
<td>917500</td>
</tr>
<tr>
<th>14</th>
<td>14</td>
<td>Thomas High School</td>
<td>Charter</td>
<td>1635</td>
<td>1043130</td>
</tr>
<tr>
<th>2</th>
<td>2</td>
<td>Shelton High School</td>
<td>Charter</td>
<td>1761</td>
<td>1056600</td>
</tr>
<tr>
<th>10</th>
<td>10</td>
<td>Wright High School</td>
<td>Charter</td>
<td>1800</td>
<td>1049400</td>
</tr>
<tr>
<th>6</th>
<td>6</td>
<td>Cabrera High School</td>
<td>Charter</td>
<td>1858</td>
<td>1081356</td>
</tr>
<tr>
<th>5</th>
<td>5</td>
<td>Wilson High School</td>
<td>Charter</td>
<td>2283</td>
<td>1319574</td>
</tr>
<tr>
<th>13</th>
<td>13</td>
<td>Ford High School</td>
<td>District</td>
<td>2739</td>
<td>1763916</td>
</tr>
<tr>
<th>0</th>
<td>0</td>
<td>Huang High School</td>
<td>District</td>
<td>2917</td>
<td>1910635</td>
</tr>
<tr>
<th>1</th>
<td>1</td>
<td>Figueroa High School</td>
<td>District</td>
<td>2949</td>
<td>1884411</td>
</tr>
<tr>
<th>11</th>
<td>11</td>
<td>Rodriguez High School</td>
<td>District</td>
<td>3999</td>
<td>2547363</td>
</tr>
<tr>
<th>3</th>
<td>3</td>
<td>Hernandez High School</td>
<td>District</td>
<td>4635</td>
<td>3022020</td>
</tr>
<tr>
<th>12</th>
<td>12</td>
<td>Johnson High School</td>
<td>District</td>
<td>4761</td>
<td>3094650</td>
</tr>
<tr>
<th>7</th>
<td>7</td>
<td>Bailey High School</td>
<td>District</td>
<td>4976</td>
<td>3124928</td>
</tr>
</tbody>
</table>
</div>




```python
#check out students file
students_df.head()
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Student ID</th>
<th>name</th>
<th>gender</th>
<th>grade</th>
<th>school</th>
<th>reading_score</th>
<th>math_score</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>0</td>
<td>Paul Bradley</td>
<td>M</td>
<td>9th</td>
<td>Huang High School</td>
<td>66</td>
<td>79</td>
</tr>
<tr>
<th>1</th>
<td>1</td>
<td>Victor Smith</td>
<td>M</td>
<td>12th</td>
<td>Huang High School</td>
<td>94</td>
<td>61</td>
</tr>
<tr>
<th>2</th>
<td>2</td>
<td>Kevin Rodriguez</td>
<td>M</td>
<td>12th</td>
<td>Huang High School</td>
<td>90</td>
<td>60</td>
</tr>
<tr>
<th>3</th>
<td>3</td>
<td>Dr. Richard Scott</td>
<td>M</td>
<td>12th</td>
<td>Huang High School</td>
<td>67</td>
<td>58</td>
</tr>
<tr>
<th>4</th>
<td>4</td>
<td>Bonnie Ray</td>
<td>F</td>
<td>9th</td>
<td>Huang High School</td>
<td>97</td>
<td>84</td>
</tr>
</tbody>
</table>
</div>



# District Summary


```python
#Extract and store all the desired quantities
num_schools = len(schools_df)
num_students = len(students_df)
total_budget = schools_df['budget'].sum()
avg_math_score = students_df["math_score"].sum()/num_students
avg_reading_score = students_df["reading_score"].sum()/num_students
perc_pass_math = 100*len(students_df.loc[students_df["math_score"] >= 70, :])/num_students
perc_pass_read = 100*len(students_df.loc[students_df["reading_score"] >= 70, :])/num_students
pass_rate = (perc_pass_math + perc_pass_read)/2

```


```python
district_summary = pd.DataFrame([{"Number of Schools": num_schools,
"Total Students": num_students,
"Total Budget": total_budget,
"Average Math Score": avg_math_score,
"Average Reading Score": avg_reading_score,
"% Passing Math": perc_pass_math,
"% Passing Reading": perc_pass_read,
"% Overall Pass Rate": pass_rate}])
district_summary = district_summary[ ["Number of Schools",
"Total Students",
"Total Budget",
"Average Math Score",
"Average Reading Score",
"% Passing Math",
"% Passing Reading",
"% Overall Pass Rate"] ]
district_summary["Total Budget"] = district_summary["Total Budget"].map("${:,.2f}".format)
district_summary["Total Students"] = district_summary["Total Students"].map("{:,}".format)

district_summary

```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Number of Schools</th>
<th>Total Students</th>
<th>Total Budget</th>
<th>Average Math Score</th>
<th>Average Reading Score</th>
<th>% Passing Math</th>
<th>% Passing Reading</th>
<th>% Overall Pass Rate</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>15</td>
<td>39,170</td>
<td>$24,649,428.00</td>
<td>78.985371</td>
<td>81.87784</td>
<td>74.980853</td>
<td>85.805463</td>
<td>80.393158</td>
</tr>
</tbody>
</table>
</div>



# School Summary


```python
schools_in_merge = schools_df.copy()
schools_in_merge["per_student_budget"] = schools_in_merge["budget"]/schools_in_merge["size"]

students_in_merge = students_df.copy()


"""
Create two columns with 1 if passing math/reading; 0 if not. Summing gives number passing; divide by number of
students to get percent.
"""
#Could do this with binning
students_in_merge["pass_reading"] = students_in_merge["reading_score"].map( lambda x: 1 if x > 70 else 0 )
students_in_merge["pass_math"] = students_in_merge["math_score"].map( lambda x: 1 if x > 70 else 0 )
students_in_merge = students_in_merge.groupby(["school"]).sum()
students_in_merge = students_in_merge[ ['reading_score','math_score','pass_reading','pass_math'] ]
students_in_merge = students_in_merge.reset_index()
students_in_merge = students_in_merge.rename(columns = {'school':'name'})

"""
Merge tables and normalize columns to get averages and percentages
"""
school_summary = pd.merge(schools_in_merge, students_in_merge, on = 'name')
school_summary['math_score'] = school_summary['math_score' ]/school_summary['size']
school_summary['reading_score'] = school_summary['reading_score' ]/school_summary['size']
school_summary['pass_reading'] = 100 * school_summary['pass_reading' ]/school_summary['size']
school_summary['pass_math'] = 100 * school_summary['pass_math' ]/school_summary['size']
school_summary['pass_rate'] = (school_summary['pass_math'] + school_summary['pass_reading'])*0.5

school_summary = school_summary.set_index("name")
school_summary.drop(['School ID'], axis = 1, inplace = True)

school_summary = school_summary.rename( columns = {"type" : "School Type",
"size": "Total Students",
"budget": "Total School Budget",
"per_student_budget": "Per Student Budget",
"reading_score":"Average Reading Score",
"math_score":"Average Math Score",
"pass_reading":"% Passing Reading",
"pass_math": "% Passing Math",
"pass_rate":"% Overall Passing Rate"} )

school_summary["Total School Budget"] = school_summary["Total School Budget"].map("${:,.2f}".format)
school_summary["Per Student Budget"] = school_summary["Per Student Budget"].map("${:,.2f}".format)
school_summary["Total Students"] = school_summary["Total Students"].map("{:,}".format)


school_summary
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>School Type</th>
<th>Total Students</th>
<th>Total School Budget</th>
<th>Per Student Budget</th>
<th>Average Reading Score</th>
<th>Average Math Score</th>
<th>% Passing Reading</th>
<th>% Passing Math</th>
<th>% Overall Passing Rate</th>
</tr>
<tr>
<th>name</th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>Huang High School</th>
<td>District</td>
<td>2,917</td>
<td>$1,910,635.00</td>
<td>$655.00</td>
<td>81.182722</td>
<td>76.629414</td>
<td>78.813850</td>
<td>63.318478</td>
<td>71.066164</td>
</tr>
<tr>
<th>Figueroa High School</th>
<td>District</td>
<td>2,949</td>
<td>$1,884,411.00</td>
<td>$639.00</td>
<td>81.158020</td>
<td>76.711767</td>
<td>78.433367</td>
<td>63.750424</td>
<td>71.091896</td>
</tr>
<tr>
<th>Shelton High School</th>
<td>Charter</td>
<td>1,761</td>
<td>$1,056,600.00</td>
<td>$600.00</td>
<td>83.725724</td>
<td>83.359455</td>
<td>92.617831</td>
<td>89.892107</td>
<td>91.254969</td>
</tr>
<tr>
<th>Hernandez High School</th>
<td>District</td>
<td>4,635</td>
<td>$3,022,020.00</td>
<td>$652.00</td>
<td>80.934412</td>
<td>77.289752</td>
<td>78.187702</td>
<td>64.746494</td>
<td>71.467098</td>
</tr>
<tr>
<th>Griffin High School</th>
<td>Charter</td>
<td>1,468</td>
<td>$917,500.00</td>
<td>$625.00</td>
<td>83.816757</td>
<td>83.351499</td>
<td>93.392371</td>
<td>89.713896</td>
<td>91.553134</td>
</tr>
<tr>
<th>Wilson High School</th>
<td>Charter</td>
<td>2,283</td>
<td>$1,319,574.00</td>
<td>$578.00</td>
<td>83.989488</td>
<td>83.274201</td>
<td>93.254490</td>
<td>90.932983</td>
<td>92.093736</td>
</tr>
<tr>
<th>Cabrera High School</th>
<td>Charter</td>
<td>1,858</td>
<td>$1,081,356.00</td>
<td>$582.00</td>
<td>83.975780</td>
<td>83.061895</td>
<td>93.864370</td>
<td>89.558665</td>
<td>91.711518</td>
</tr>
<tr>
<th>Bailey High School</th>
<td>District</td>
<td>4,976</td>
<td>$3,124,928.00</td>
<td>$628.00</td>
<td>81.033963</td>
<td>77.048432</td>
<td>79.300643</td>
<td>64.630225</td>
<td>71.965434</td>
</tr>
<tr>
<th>Holden High School</th>
<td>Charter</td>
<td>427</td>
<td>$248,087.00</td>
<td>$581.00</td>
<td>83.814988</td>
<td>83.803279</td>
<td>92.740047</td>
<td>90.632319</td>
<td>91.686183</td>
</tr>
<tr>
<th>Pena High School</th>
<td>Charter</td>
<td>962</td>
<td>$585,858.00</td>
<td>$609.00</td>
<td>84.044699</td>
<td>83.839917</td>
<td>92.203742</td>
<td>91.683992</td>
<td>91.943867</td>
</tr>
<tr>
<th>Wright High School</th>
<td>Charter</td>
<td>1,800</td>
<td>$1,049,400.00</td>
<td>$583.00</td>
<td>83.955000</td>
<td>83.682222</td>
<td>93.444444</td>
<td>90.277778</td>
<td>91.861111</td>
</tr>
<tr>
<th>Rodriguez High School</th>
<td>District</td>
<td>3,999</td>
<td>$2,547,363.00</td>
<td>$637.00</td>
<td>80.744686</td>
<td>76.842711</td>
<td>77.744436</td>
<td>64.066017</td>
<td>70.905226</td>
</tr>
<tr>
<th>Johnson High School</th>
<td>District</td>
<td>4,761</td>
<td>$3,094,650.00</td>
<td>$650.00</td>
<td>80.966394</td>
<td>77.072464</td>
<td>78.281874</td>
<td>63.852132</td>
<td>71.067003</td>
</tr>
<tr>
<th>Ford High School</th>
<td>District</td>
<td>2,739</td>
<td>$1,763,916.00</td>
<td>$644.00</td>
<td>80.746258</td>
<td>77.102592</td>
<td>77.510040</td>
<td>65.753925</td>
<td>71.631982</td>
</tr>
<tr>
<th>Thomas High School</th>
<td>Charter</td>
<td>1,635</td>
<td>$1,043,130.00</td>
<td>$638.00</td>
<td>83.848930</td>
<td>83.418349</td>
<td>92.905199</td>
<td>90.214067</td>
<td>91.559633</td>
</tr>
</tbody>
</table>
</div>



# Top Performing Schools


```python
top_schools = school_summary.sort_values(by = ["% Overall Passing Rate"], ascending = False).head(5)
top_schools
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>School Type</th>
<th>Total Students</th>
<th>Total School Budget</th>
<th>Per Student Budget</th>
<th>Average Reading Score</th>
<th>Average Math Score</th>
<th>% Passing Reading</th>
<th>% Passing Math</th>
<th>% Overall Passing Rate</th>
</tr>
<tr>
<th>name</th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>Wilson High School</th>
<td>Charter</td>
<td>2,283</td>
<td>$1,319,574.00</td>
<td>$578.00</td>
<td>83.989488</td>
<td>83.274201</td>
<td>93.254490</td>
<td>90.932983</td>
<td>92.093736</td>
</tr>
<tr>
<th>Pena High School</th>
<td>Charter</td>
<td>962</td>
<td>$585,858.00</td>
<td>$609.00</td>
<td>84.044699</td>
<td>83.839917</td>
<td>92.203742</td>
<td>91.683992</td>
<td>91.943867</td>
</tr>
<tr>
<th>Wright High School</th>
<td>Charter</td>
<td>1,800</td>
<td>$1,049,400.00</td>
<td>$583.00</td>
<td>83.955000</td>
<td>83.682222</td>
<td>93.444444</td>
<td>90.277778</td>
<td>91.861111</td>
</tr>
<tr>
<th>Cabrera High School</th>
<td>Charter</td>
<td>1,858</td>
<td>$1,081,356.00</td>
<td>$582.00</td>
<td>83.975780</td>
<td>83.061895</td>
<td>93.864370</td>
<td>89.558665</td>
<td>91.711518</td>
</tr>
<tr>
<th>Holden High School</th>
<td>Charter</td>
<td>427</td>
<td>$248,087.00</td>
<td>$581.00</td>
<td>83.814988</td>
<td>83.803279</td>
<td>92.740047</td>
<td>90.632319</td>
<td>91.686183</td>
</tr>
</tbody>
</table>
</div>



# Bottom Performing Schools


```python
bottom_schools = school_summary.sort_values(by = ["% Overall Passing Rate"], ascending = True).head(5)
bottom_schools
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>School Type</th>
<th>Total Students</th>
<th>Total School Budget</th>
<th>Per Student Budget</th>
<th>Average Reading Score</th>
<th>Average Math Score</th>
<th>% Passing Reading</th>
<th>% Passing Math</th>
<th>% Overall Passing Rate</th>
</tr>
<tr>
<th>name</th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>Rodriguez High School</th>
<td>District</td>
<td>3,999</td>
<td>$2,547,363.00</td>
<td>$637.00</td>
<td>80.744686</td>
<td>76.842711</td>
<td>77.744436</td>
<td>64.066017</td>
<td>70.905226</td>
</tr>
<tr>
<th>Huang High School</th>
<td>District</td>
<td>2,917</td>
<td>$1,910,635.00</td>
<td>$655.00</td>
<td>81.182722</td>
<td>76.629414</td>
<td>78.813850</td>
<td>63.318478</td>
<td>71.066164</td>
</tr>
<tr>
<th>Johnson High School</th>
<td>District</td>
<td>4,761</td>
<td>$3,094,650.00</td>
<td>$650.00</td>
<td>80.966394</td>
<td>77.072464</td>
<td>78.281874</td>
<td>63.852132</td>
<td>71.067003</td>
</tr>
<tr>
<th>Figueroa High School</th>
<td>District</td>
<td>2,949</td>
<td>$1,884,411.00</td>
<td>$639.00</td>
<td>81.158020</td>
<td>76.711767</td>
<td>78.433367</td>
<td>63.750424</td>
<td>71.091896</td>
</tr>
<tr>
<th>Hernandez High School</th>
<td>District</td>
<td>4,635</td>
<td>$3,022,020.00</td>
<td>$652.00</td>
<td>80.934412</td>
<td>77.289752</td>
<td>78.187702</td>
<td>64.746494</td>
<td>71.467098</td>
</tr>
</tbody>
</table>
</div>



# Math Scores By Grade


```python
math_students = students_df.copy()
math_students['number_of_students'] = 1
math_grades = math_students.groupby(["school", "grade"]).sum()
math_grades = math_grades[ ['number_of_students','math_score'] ]
math_grades = math_grades.reset_index()
math_grades['math_score'] = math_grades['math_score']/math_grades['number_of_students']
math_grades = math_grades.pivot(index = 'school', columns = 'grade', values = 'math_score')
math_grades
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th>grade</th>
<th>10th</th>
<th>11th</th>
<th>12th</th>
<th>9th</th>
</tr>
<tr>
<th>school</th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>Bailey High School</th>
<td>76.996772</td>
<td>77.515588</td>
<td>76.492218</td>
<td>77.083676</td>
</tr>
<tr>
<th>Cabrera High School</th>
<td>83.154506</td>
<td>82.765560</td>
<td>83.277487</td>
<td>83.094697</td>
</tr>
<tr>
<th>Figueroa High School</th>
<td>76.539974</td>
<td>76.884344</td>
<td>77.151369</td>
<td>76.403037</td>
</tr>
<tr>
<th>Ford High School</th>
<td>77.672316</td>
<td>76.918058</td>
<td>76.179963</td>
<td>77.361345</td>
</tr>
<tr>
<th>Griffin High School</th>
<td>84.229064</td>
<td>83.842105</td>
<td>83.356164</td>
<td>82.044010</td>
</tr>
<tr>
<th>Hernandez High School</th>
<td>77.337408</td>
<td>77.136029</td>
<td>77.186567</td>
<td>77.438495</td>
</tr>
<tr>
<th>Holden High School</th>
<td>83.429825</td>
<td>85.000000</td>
<td>82.855422</td>
<td>83.787402</td>
</tr>
<tr>
<th>Huang High School</th>
<td>75.908735</td>
<td>76.446602</td>
<td>77.225641</td>
<td>77.027251</td>
</tr>
<tr>
<th>Johnson High School</th>
<td>76.691117</td>
<td>77.491653</td>
<td>76.863248</td>
<td>77.187857</td>
</tr>
<tr>
<th>Pena High School</th>
<td>83.372000</td>
<td>84.328125</td>
<td>84.121547</td>
<td>83.625455</td>
</tr>
<tr>
<th>Rodriguez High School</th>
<td>76.612500</td>
<td>76.395626</td>
<td>77.690748</td>
<td>76.859966</td>
</tr>
<tr>
<th>Shelton High School</th>
<td>82.917411</td>
<td>83.383495</td>
<td>83.778976</td>
<td>83.420755</td>
</tr>
<tr>
<th>Thomas High School</th>
<td>83.087886</td>
<td>83.498795</td>
<td>83.497041</td>
<td>83.590022</td>
</tr>
<tr>
<th>Wilson High School</th>
<td>83.724422</td>
<td>83.195326</td>
<td>83.035794</td>
<td>83.085578</td>
</tr>
<tr>
<th>Wright High School</th>
<td>84.010288</td>
<td>83.836782</td>
<td>83.644986</td>
<td>83.264706</td>
</tr>
</tbody>
</table>
</div>



# Reading Scores By Grade


```python
reading_students = students_df.copy()
reading_students['number_of_students'] = 1
reading_grades = reading_students.groupby(["school", "grade"]).sum()
reading_grades = reading_grades[ ['number_of_students','reading_score'] ]
reading_grades = reading_grades.reset_index()
reading_grades['reading_score'] = reading_grades['reading_score']/reading_grades['number_of_students']
reading_grades.pivot(index = 'school', columns = 'grade', values = 'reading_score')
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th>grade</th>
<th>10th</th>
<th>11th</th>
<th>12th</th>
<th>9th</th>
</tr>
<tr>
<th>school</th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>Bailey High School</th>
<td>80.907183</td>
<td>80.945643</td>
<td>80.912451</td>
<td>81.303155</td>
</tr>
<tr>
<th>Cabrera High School</th>
<td>84.253219</td>
<td>83.788382</td>
<td>84.287958</td>
<td>83.676136</td>
</tr>
<tr>
<th>Figueroa High School</th>
<td>81.408912</td>
<td>80.640339</td>
<td>81.384863</td>
<td>81.198598</td>
</tr>
<tr>
<th>Ford High School</th>
<td>81.262712</td>
<td>80.403642</td>
<td>80.662338</td>
<td>80.632653</td>
</tr>
<tr>
<th>Griffin High School</th>
<td>83.706897</td>
<td>84.288089</td>
<td>84.013699</td>
<td>83.369193</td>
</tr>
<tr>
<th>Hernandez High School</th>
<td>80.660147</td>
<td>81.396140</td>
<td>80.857143</td>
<td>80.866860</td>
</tr>
<tr>
<th>Holden High School</th>
<td>83.324561</td>
<td>83.815534</td>
<td>84.698795</td>
<td>83.677165</td>
</tr>
<tr>
<th>Huang High School</th>
<td>81.512386</td>
<td>81.417476</td>
<td>80.305983</td>
<td>81.290284</td>
</tr>
<tr>
<th>Johnson High School</th>
<td>80.773431</td>
<td>80.616027</td>
<td>81.227564</td>
<td>81.260714</td>
</tr>
<tr>
<th>Pena High School</th>
<td>83.612000</td>
<td>84.335938</td>
<td>84.591160</td>
<td>83.807273</td>
</tr>
<tr>
<th>Rodriguez High School</th>
<td>80.629808</td>
<td>80.864811</td>
<td>80.376426</td>
<td>80.993127</td>
</tr>
<tr>
<th>Shelton High School</th>
<td>83.441964</td>
<td>84.373786</td>
<td>82.781671</td>
<td>84.122642</td>
</tr>
<tr>
<th>Thomas High School</th>
<td>84.254157</td>
<td>83.585542</td>
<td>83.831361</td>
<td>83.728850</td>
</tr>
<tr>
<th>Wilson High School</th>
<td>84.021452</td>
<td>83.764608</td>
<td>84.317673</td>
<td>83.939778</td>
</tr>
<tr>
<th>Wright High School</th>
<td>83.812757</td>
<td>84.156322</td>
<td>84.073171</td>
<td>83.833333</td>
</tr>
</tbody>
</table>
</div>



# Scores by School Spending


```python
student_group = students_df.copy()
student_group["pass_reading"] = student_group["reading_score"].map( lambda x: 1 if x > 70 else 0 )
student_group["pass_math"] = student_group["math_score"].map( lambda x: 1 if x > 70 else 0 )
student_group['number_of_students'] = 1
student_group = student_group.groupby(['school']).sum()
student_group[ ['reading_score', 'math_score', 'pass_reading', 'pass_math', 'number_of_students'] ]
student_group = student_group.reset_index()
student_group = student_group.rename(columns = {'school':'name'})

schools_spend = schools_df.copy()
schools_spend["per_student_budget"] = schools_spend["budget"]/schools_spend["size"]

spend_summary = pd.merge(student_group, schools_spend, on = "name")
spend_summary = spend_summary[ [ 'name','reading_score',
'math_score','pass_reading',
'pass_math','number_of_students','per_student_budget' ] ]

bins = [0, 600, 628, 644, 660]
bin_label = ["<600", ' 600 - 628', '628 - 644', '644 - 660']
spend_summary['Spending Range($)'] =  pd.cut(spend_summary['per_student_budget'], bins, labels = bin_label )
spend_summary = spend_summary[ ['reading_score',
'math_score',
'pass_reading',
'pass_math',
'number_of_students',
'per_student_budget',
'Spending Range($)'] ]


spend_summary = spend_summary.groupby(['Spending Range($)']).sum()
spend_summary['reading_score'] = spend_summary['reading_score']/spend_summary['number_of_students']
spend_summary['math_score'] = spend_summary['math_score']/spend_summary['number_of_students']
spend_summary['pass_reading'] = 100 * spend_summary['pass_reading']/spend_summary['number_of_students']
spend_summary['pass_math'] = 100 * spend_summary['pass_math']/spend_summary['number_of_students']
spend_summary['pass_rate'] = 0.5 * (spend_summary['pass_reading'] + spend_summary['pass_math'] )
spend_summary = spend_summary[['math_score', 'reading_score', 'pass_math', 'pass_reading', 'pass_rate']]

spend_summary = spend_summary.rename(columns = {"math_score": "Average Math Score",
"reading_score": "Average Reading Score",
"pass_math": "% Passing Math",
"pass_reading":"% Passing Reading",
"pass_rate":"% Overall Pass Rate"} )


spend_summary
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Average Math Score</th>
<th>Average Reading Score</th>
<th>% Passing Math</th>
<th>% Passing Reading</th>
<th>% Overall Pass Rate</th>
</tr>
<tr>
<th>Spending Range($)</th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>&lt;600</th>
<td>83.362283</td>
<td>83.912412</td>
<td>90.232501</td>
<td>93.271005</td>
<td>91.751753</td>
</tr>
<tr>
<th>600 - 628</th>
<td>79.179989</td>
<td>81.976641</td>
<td>73.116392</td>
<td>83.769916</td>
<td>78.443154</td>
</tr>
<tr>
<th>628 - 644</th>
<td>77.821056</td>
<td>81.301007</td>
<td>68.168168</td>
<td>80.056527</td>
<td>74.112348</td>
</tr>
<tr>
<th>644 - 660</th>
<td>77.049297</td>
<td>81.005604</td>
<td>64.062373</td>
<td>78.372452</td>
<td>71.217412</td>
</tr>
</tbody>
</table>
</div>



# Scores by School Size


```python
student_group = students_df.copy()
student_group["pass_reading"] = student_group["reading_score"].map( lambda x: 1 if x > 70 else 0 )
student_group["pass_math"] = student_group["math_score"].map( lambda x: 1 if x > 70 else 0 )
student_group['number_of_students'] = 1
student_group = student_group.groupby(['school']).sum()
student_group[ ['reading_score', 'math_score', 'pass_reading', 'pass_math', 'number_of_students'] ]
student_group = student_group.reset_index()
student_group = student_group.rename(columns = {'school':'name'})

schools_spend = schools_df.copy()
schools_spend["per_student_budget"] = schools_spend["budget"]/schools_spend["size"]

size_summary = pd.merge(student_group, schools_spend, on = "name")
size_summary = size_summary[ [ 'name','reading_score',
'math_score','pass_reading',
'pass_math','number_of_students','per_student_budget', 'size' ] ]


bins = [0, 1800, 3000, 5000]
bin_label = ['Small(<1800)', 'Medium(1800 - 3000)', 'Large(3000 - 5000)']
size_summary['School Size'] =  pd.cut(size_summary['size'], bins, labels = bin_label )
size_summary = size_summary[ ['reading_score',
'math_score',
'pass_reading',
'pass_math',
'number_of_students',
'School Size'] ]

size_summary = size_summary.groupby(['School Size']).sum()
size_summary['reading_score'] = size_summary['reading_score']/size_summary['number_of_students']
size_summary['math_score'] = size_summary['math_score']/size_summary['number_of_students']
size_summary['pass_reading'] = 100 * size_summary['pass_reading']/size_summary['number_of_students']
size_summary['pass_math'] = 100 * size_summary['pass_math']/size_summary['number_of_students']
size_summary['pass_rate'] = 0.5 * (size_summary['pass_reading'] + size_summary['pass_math'] )
size_summary = size_summary[['math_score', 'reading_score', 'pass_math', 'pass_reading', 'pass_rate']]

size_summary = size_summary.rename(columns = {"math_score": "Average Math Score",
"reading_score": "Average Reading Score",
"pass_math":"% Passing Math",
"pass_reading":"% Passing Reading",
"pass_rate":"% Overall Pass Rate"})

size_summary
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Average Math Score</th>
<th>Average Reading Score</th>
<th>% Passing Math</th>
<th>% Passing Reading</th>
<th>% Overall Pass Rate</th>
</tr>
<tr>
<th>School Size</th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>Small(&lt;1800)</th>
<td>83.523035</td>
<td>83.861418</td>
<td>90.264498</td>
<td>92.959146</td>
<td>91.611822</td>
</tr>
<tr>
<th>Medium(1800 - 3000)</th>
<td>78.878001</td>
<td>81.993096</td>
<td>72.713008</td>
<td>83.226110</td>
<td>77.969559</td>
</tr>
<tr>
<th>Large(3000 - 5000)</th>
<td>77.070764</td>
<td>80.928365</td>
<td>64.335093</td>
<td>78.417070</td>
<td>71.376082</td>
</tr>
</tbody>
</table>
</div>



# Scores By School Type


```python
student_group = students_df.copy()
student_group["pass_reading"] = student_group["reading_score"].map( lambda x: 1 if x > 70 else 0 )
student_group["pass_math"] = student_group["math_score"].map( lambda x: 1 if x > 70 else 0 )
student_group['number_of_students'] = 1
student_group = student_group.groupby(['school']).sum()
student_group[ ['reading_score', 'math_score', 'pass_reading', 'pass_math', 'number_of_students'] ]
student_group = student_group.reset_index()
student_group = student_group.rename(columns = {'school':'name'})

schools_spend = schools_df.copy()
schools_spend["per_student_budget"] = schools_spend["budget"]/schools_spend["size"]

type_summary = pd.merge(student_group, schools_spend, on = "name")
type_summary = type_summary[ [ 'name','reading_score',
'math_score','pass_reading',
'pass_math','type', 'size' ] ]

type_summary = type_summary.groupby(['type']).sum()
type_summary['reading_score'] = type_summary['reading_score']/type_summary['size']
type_summary['math_score'] = type_summary['math_score']/type_summary['size']
type_summary['pass_reading'] = 100*type_summary['pass_reading']/type_summary['size']
type_summary['pass_math'] = 100*type_summary['pass_math']/type_summary['size']
type_summary['pass_rate'] = 0.5*(type_summary['pass_math'] + type_summary['pass_reading'])

type_summary = type_summary.rename(columns = {"reading_score": "Average Reading Score",
"math_score": "Average Math Score",
"pass_reading":"% Passing Reading",
"pass_math":"% Passing Math",
"size":"Number of Students",
"pass_rate":"% Overall Pass Rate"} )



type_summary
```




<div>
<style>
.dataframe thead tr:only-child th {
text-align: right;
}

.dataframe thead th {
text-align: left;
}

.dataframe tbody tr th {
vertical-align: top;
}
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Average Reading Score</th>
<th>Average Math Score</th>
<th>% Passing Reading</th>
<th>% Passing Math</th>
<th>Number of Students</th>
<th>% Overall Pass Rate</th>
</tr>
<tr>
<th>type</th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>Charter</th>
<td>83.902821</td>
<td>83.406183</td>
<td>93.152370</td>
<td>90.282106</td>
<td>12194</td>
<td>91.717238</td>
</tr>
<tr>
<th>District</th>
<td>80.962485</td>
<td>76.987026</td>
<td>78.369662</td>
<td>64.305308</td>
<td>26976</td>
<td>71.337485</td>
</tr>
</tbody>
</table>
</div>



## Summary

Charter schools have an overall pass rate about 20 percent larger than those of district schools.
As the size of the school increases, the overall pass rate decreases.
The top 5 performing schools are all charter schools, while the bottom 5 performing schools are all district schools.

