# Aurora Compromise (SQL)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/sql1-challenge.PNG/>
</p>

> DEADFACE has taken responsibility for a partial database hack on a pharmacy tied to Aurora Pharmaceuticals. The hacked data consists of patient data, staff data, and information on drugs and prescriptions.

> We’ve managed to get a hold of the hacked data. Provide the first and last name of the patient that lives on a street called Hansons Terrace.

> Submit the flag as: flag{First Last}.

You are given a PDF file.

## Solution

In the PDF I found the patient database that holds the addresses.

<p align="left">
  <img height=500 img src=./readme_assets/sql1-pdf.PNG/>
</p>

Search for `Hansons Terrace` in the SQL file to get the flag.

<p align="left">
  <img height=500 img src=./readme_assets/sql1-flag.PNG/>
</p>

## Flag

**`flag{Sandor Beyer}`**

## Tools





