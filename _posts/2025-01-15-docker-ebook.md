---
layout: post
title: PROBLEM SOLVE
subtitle: problem solving day1
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [problem solbing, Java]
comments: true
mathjax: false
author: Noor
---

#  Solution Guide

## 1. Problem Solving

###  BEE 1004-Simple Product
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EPUB Viewer</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            overflow: hidden;
        }
        #epub-container {
            width: 100%;
            height: 100vh;
            overflow: auto;
            border: 1px solid #ddd;
        }
        #controls {
            display: flex;
            justify-content: center;
            padding: 10px;
            background-color: #f9f9f9;
            border-bottom: 1px solid #ddd;
        }
        button {
            margin: 0 5px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/epubjs/dist/epub.min.js"></script>
</head>
<body>
    <div id="controls">
        <button id="prev-btn">Previous</button>
        <button id="next-btn">Next</button>
    </div>
    <div id="epub-container"></div>

    <script>
        const epubContainer = document.getElementById('epub-container');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');

        let rendition;

        // Load a static EPUB file
        const staticFileUrl = 'ebook\Introduction-to-Docker-A-Beginner_s-Guide.epub';
        const book = ePub(staticFileUrl);
        rendition = book.renderTo(epubContainer, {
            width: '100%',
            height: '100vh'
        });
        rendition.display();

        prevBtn.addEventListener('click', () => {
            if (rendition) rendition.prev();
        });

        nextBtn.addEventListener('click', () => {
            if (rendition) rendition.next();
        });
    </script>
</body>
</html>

```

### Solution 
```typescript

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read two integer values
        int A = scanner.nextInt();
        int B = scanner.nextInt();

        // Calculate the product
        int PROD = A * B;

        // Print the result in the required format
        System.out.println("PROD = " + PROD);

        scanner.close();
    }
}


```
## 2. Problem Solving

###  BEE 1005-Average 1
```html
Read two floating points' values of double precision A and B, corresponding to two student's grades. After this, calculate the student's average, considering that grade A has weight 3.5 and B has weight 7.5. Each grade can be from zero to ten, always with one digit after the decimal point. Don’t forget to print the end of line after the result, otherwise you will receive “Presentation Error”. Don’t forget the space before and after the equal sign.

Input
The input file contains 2 floating points' values with one digit after the decimal point.

Output
Print the message "MEDIA"(average in Portuguese) and the student's average according to the following example, with 5 digits after the decimal point and with a blank space before and after the equal signal.
MEDIA= 3.5+7.5/ (A×3.5)+(B×7.5)
​
 

```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read two floating-point values
        double A = scanner.nextDouble();
        double B = scanner.nextDouble();

        // Define the weights
        double weightA = 3.5;
        double weightB = 7.5;

        // Calculate the weighted average
        double MEDIA = ((A * weightA) + (B * weightB)) / (weightA + weightB);

        // Print the result with the required format
        System.out.printf("MEDIA = %.5f%n", MEDIA);

        scanner.close();
    }
}


```

## 3. Problem Solving

###  BEE 1007-Difference
```html
Read four integer values named A, B, C and D. Calculate and print the difference of product A and B by the product of C and D (A * B - C * D).

Input
The input file contains 4 integer values.

Output
Print DIFERENCA (DIFFERENCE in Portuguese) with all the capital letters, according to the following example, with a blank space before and after the equal signal.
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read four integer values
        int A = scanner.nextInt();
        int B = scanner.nextInt();
        int C = scanner.nextInt();
        int D = scanner.nextInt();

        // Calculate the difference
        int DIFERENCA = (A * B) - (C * D);

        // Print the result in the required format
        System.out.println("DIFERENCA = " + DIFERENCA);

        scanner.close();
    }
}


```
## 4. Problem Solving

###  BEE 1007-Salary
```html
Write a program that reads an employee's number, his/her worked hours number in a month and the amount he received per hour. Print the employee's number and salary that he/she will receive at end of the month, with two decimal places.

Don’t forget to print the line's end after the result, otherwise you will receive “Presentation Error”.
Don’t forget the space before and after the equal signal and after the U$.
Input
The input file contains 2 integer numbers and 1 value of floating point, representing the number, worked hours amount and the amount the employee receives per worked hour.

Output
Print the number and the employee's salary, according to the given example, with a blank space before and after the equal signal.
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the employee's number
        int employeeNumber = scanner.nextInt();

        // Read the number of hours worked in a month
        int workedHours = scanner.nextInt();

        // Read the amount received per hour
        double amountPerHour = scanner.nextDouble();

        // Calculate the salary
        double salary = workedHours * amountPerHour;

        // Print the employee's number and salary with the required format
        System.out.printf("NUMBER = %d%n", employeeNumber);
        System.out.printf("SALARY = U$ %.2f%n", salary);

        scanner.close();
    }
}
```
## 6. Problem Solving

###  BEE 1009-Salary with Bonus
```html
Make a program that reads a seller's name, his/her fixed salary and the sale's total made by himself/herself in the month (in money). Considering that this seller receives 15% over all products sold, write the final salary (total) of this seller at the end of the month , with two decimal places.

- Don’t forget to print the line's end after the result, otherwise you will receive “Presentation Error”.

- Don’t forget the blank spaces.

Input
The input file contains a text (employee's first name), and two double precision values, that are the seller's salary and the total value sold by him/her.

Output
Print the seller's total salary, according to the given example.
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the seller's name
        String name = scanner.nextLine();

        // Read the seller's fixed salary and total sales
        double fixedSalary = scanner.nextDouble();
        double totalSales = scanner.nextDouble();

        // Calculate the commission (15% of total sales)
        double commission = totalSales * 0.15;

        // Calculate the final salary (fixed salary + commission)
        double totalSalary = fixedSalary + commission;

        // Print the seller's total salary with two decimal places
        System.out.printf("TOTAL = R$ %.2f%n", totalSalary);

        scanner.close();
    }
}

```
## 7. Problem Solving

###  BEE 1010-Simple Calculate
```html
In this problem, the task is to read a code of a product 1, the number of units of product 1, the price for one unit of product 1, the code of a product 2, the number of units of product 2 and the price for one unit of product 2. After this, calculate and show the amount to be paid.

Input
The input file contains two lines of data. In each line there will be 3 values: two integers and a floating value with 2 digits after the decimal point.

Output
The output file must be a message like the following example where "Valor a pagar" means Value to Pay. Remember the space after ":" and after "R$" symbol. The value must be presented with 2 digits after the point.
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the first product's data (code, quantity, price)
        int code1 = scanner.nextInt();
        int quantity1 = scanner.nextInt();
        double price1 = scanner.nextDouble();

        // Read the second product's data (code, quantity, price)
        int code2 = scanner.nextInt();
        int quantity2 = scanner.nextInt();
        double price2 = scanner.nextDouble();

        // Calculate the total price for both products
        double totalToPay = (quantity1 * price1) + (quantity2 * price2);

        // Print the result with the required format using printf
        System.out.printf("Valor a pagar: R$ %.2f%n", totalToPay);

        scanner.close();
    }
}



```
## 8. Problem Solving

###  BEE 1011-Sphere
```html

Make a program that calculates and shows the volume of a sphere being provided the value of its radius (R) . The formula to calculate the volume is: (4/3) * pi * R3. Consider (assign) for pi the value 3.14159.

Tip: Use (4/3.0) or (4.0/3) in your formula, because some languages (including C++) assume that the division's result between two integers is another integer. :)

Input
The input contains a value of floating point (double precision).

Output
The output must be a message "VOLUME" like the following example with a space before and after the equal signal. The value must be presented with 3 digits after the decimal point.
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the radius (R) of the sphere
        double radius = scanner.nextDouble();

        // Define the value of pi
        double pi = 3.14159;

        // Calculate the volume of the sphere
        double volume = (4.0 / 3) * pi * Math.pow(radius, 3);

        // Print the result with 3 digits after the decimal point
        System.out.printf("VOLUME = %.3f%n", volume);

        scanner.close();
    }
}



```
## 12. Problem Solving

###  BEE 1012-Area
```html
Make a program that reads three floating point values: A, B and C. Then, calculate and show:
a) the area of the rectangled triangle that has base A and height C.
b) the area of the radius's circle C. (pi = 3.14159)
c) the area of the trapezium which has A and B by base, and C by height.
d) the area of ​​the square that has side B.
e) the area of the rectangle that has sides A and B.

Input
The input file contains three double values with one digit after the decimal point.

Output
The output file must contain 5 lines of data. Each line corresponds to one of the areas described above, always with a corresponding message (in Portuguese) and one space between the two points and the value. The value calculated must be presented with 3 digits after the decimal point.
Rectangled Triangle: The area of a right triangle is given by:

Area
=12
×
base
×
height
Area= 1/2  ×base×height


Circle: The area of a circle is calculated using:

Area
=𝜋×radius2
Area=π×radius^ 2
 
where 
𝜋
π is given as 3.14159.

Trapezium: The area of a trapezium is given by:

Area
=1/2×(base1+base2)×height

Square: The area of a square is simply:

Area
=side2
Area=side ^2
 
Rectangle: The area of a rectangle is:


Area=length×width
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the three floating point values
        double A = scanner.nextDouble();
        double B = scanner.nextDouble();
        double C = scanner.nextDouble();

        // Calculate the area of the right triangle
        double areaTriangle = (A * C) / 2.0;

        // Calculate the area of the circle
        double pi = 3.14159;
        double areaCircle = pi * Math.pow(C, 2);

        // Calculate the area of the trapezium
        double areaTrapezium = ((A + B) * C) / 2.0;

        // Calculate the area of the square
        double areaSquare = Math.pow(B, 2);

        // Calculate the area of the rectangle
        double areaRectangle = A * B;

        // Print the results with the appropriate format
        System.out.printf("TRIANGULO: %.3f%n", areaTriangle);
        System.out.printf("CIRCULO: %.3f%n", areaCircle);
        System.out.printf("TRAPEZIO: %.3f%n", areaTrapezium);
        System.out.printf("QUADRADO: %.3f%n", areaSquare);
        System.out.printf("RETANGULO: %.3f%n", areaRectangle);

        scanner.close();
    }
}


```
# 13. Problem Solving

###  BEE 1013-The Greatest
```html
Make a program that reads 3 integer values and present the greatest one followed by the message "eh o maior". Use the following formula:



Input
The input file contains 3 integer values.

Output
Print the greatest of these three values followed by a space and the message “eh o maior”.
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the three integer values
        int A = scanner.nextInt();
        int B = scanner.nextInt();
        int C = scanner.nextInt();

        // Find the greatest of the three values
        int greatest = A;
        if (B > greatest) {
            greatest = B;
        }
        if (C > greatest) {
            greatest = C;
        }

        // Print the greatest value followed by the message
        System.out.println(greatest + " eh o maior");

        scanner.close();
    }
}


```
# 14. Problem Solving

###  BEE 1014-The Consumption
```html
Calculate a car's average consumption being provided the total distance traveled (in Km) and the spent fuel total (in liters).

Input
The input file contains two values: one integer value X representing the total distance (in Km) and the second one is a floating point number Y  representing the spent fuel total, with a digit after the decimal point.

Output
Present a value that represents the average consumption of a car with 3 digits after the decimal point, followed by the message "km/
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the total distance traveled (X) and the total fuel consumed (Y)
        int X = scanner.nextInt();  // Distance in Km (integer)
        double Y = scanner.nextDouble();  // Fuel in Liters (floating-point)

        // Calculate the average consumption
        double averageConsumption = X / Y;

        // Print the result with 3 digits after the decimal point
        System.out.printf("%.3f km/l%n", averageConsumption);

        scanner.close();
    }
}


```
# 15. Problem Solving

###  BEE 1015-Distance Between Two Points
```html
Read the four values corresponding to the x and y axes of two points in the plane, p1 (x1, y1) and p2 (x2, y2) and calculate the distance between them, showing four decimal places, according to the formula:

Distance = 

Input
The input file contains two lines of data. The first one contains two double values: x1 y1 and the second one also contains two double values with one digit after the decimal point: x2 y2.

Output
Calculate and print the distance value using the provided formula, with 4 decimal places.
```

### Solution 
```typescript
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the coordinates of the first point (x1, y1)
        double x1 = scanner.nextDouble();
        double y1 = scanner.nextDouble();

        // Read the coordinates of the second point (x2, y2)
        double x2 = scanner.nextDouble();
        double y2 = scanner.nextDouble();

        // Calculate the distance using the Euclidean distance formula
        double distance = Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));

        // Print the result with 4 digits after the decimal point
        System.out.printf("%.4f%n", distance);

        scanner.close();
    }
}



```