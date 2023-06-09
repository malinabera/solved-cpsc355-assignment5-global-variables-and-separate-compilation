Download Link: https://assignmentchef.com/product/solved-cpsc355-assignment5-global-variables-and-separate-compilation
<br>



<strong>Part A:  Global Variables and Separate Compilation</strong>

Reverse Polish (or postfix) notation can be used to represent arithmetic expressions. For example, the infix expression

(1 – 2) * (4 + 5) =

is the following using reverse Polish notation:

1 2 – 4 5 + * =

Hewlett-Packard calculators often use this form of entry. The following is a C program that emulates such a calculator:

#include &lt;stdio.h&gt;

#include &lt;stdlib.h&gt;

/*  Constants  */

#define MAXOP   20

#define NUMBER  ‘0’

#define TOOBIG  ‘9’

/*  Function prototypes  */

int push(int f);

int pop();

void clear();

int getop(char *s, int lim);

int getch();

void ungetch(int c);

int main()

{

int type;

char s[MAXOP];

int op2;

while ((type = getop(s, MAXOP)) != EOF) {

switch (type) {

case NUMBER:

push(atoi(s));

break;

case ‘+’:

push(pop() + pop());

break;

case ‘*’:

push(pop() * pop());

break;

case ‘-‘:

op2 = pop();

push(pop() – op2);

break;

case ‘/’:

op2 = pop();

if (op2 != 0)

push(pop() / op2);

else

printf(“zero divisor popped
”);

break;

case ‘=’:

printf(“
%d

”, push(pop()));

break;

case ‘c’:

clear();

break;

case TOOBIG:

printf(“%.20s … is too long
”, s);

break;

default:

printf(“unknown command %c
”, type);

break;

}

}




return 0;

}







#define MAXVAL  100




int sp = 0;

int val[MAXVAL];




int push(int f)

{

if (sp &lt; MAXVAL)

return val[sp++] = f;

else {

printf(“error: stack full
”);

clear();

return 0;

}

}




int pop()

{

if (sp &gt; 0)

return val[–sp];

else {

printf(“error: stack empty
”);

clear();

return 0;

}

}




void clear()

{

sp = 0;

}




int getop(char *s, int lim)

{

int i, c;




while ((c = getch()) == ‘ ‘ || c == ‘t’ || c == ‘
’)

;

if (c &lt; ‘0’ || c &gt; ‘9’)

return c;

s[0] = c;

for (i = 1; (c = getchar()) &gt;= ‘0’ &amp;&amp; c &lt;= ‘9’; i++)

if (i &lt; lim)

s[i] = c;




if (i &lt; lim) {

ungetch(c);

s[i] = ‘ ’;

return NUMBER;

} else {

while (c != ‘
’ &amp;&amp; c != EOF)

c = getchar();

s[lim-1] = ‘ ’;

return TOOBIG;

}

}




#define BUFSIZE   100




char buf[BUFSIZE];

int bufp = 0;

int getch()

{

return bufp &gt; 0 ? buf[–bufp] : getchar();

}

void ungetch(int c)

{

if (bufp &gt; BUFSIZE)

printf(“ungetch: too many characters
”);

else

buf[bufp++] = c;

}

Translate all functions except main() into ARMv8 assembly language, and put them into a separate assembly source code file called <em>a5a.asm</em>. These functions will be called from the main() function given above, which will be in its own C source code file called <em>a5aMain.c</em>. Also move the global variables into <em>a5a.asm</em>. Your assembly functions will call the library routines printf() and getchar(). Be sure to handle the global variables and format strings in the appropriate way. Input will come from standard input; the program is terminated by typing control-d. Run the program to show that it is working as expected, capturing its output using the <em>script </em>UNIX command, and name the output file <em>script1.txt.</em> Use a variety of input expressions to show that your program is calculating correctly.

<strong>Part B:  External Pointer Arrays and Command-Line Arguments</strong>

Given the following declaration in C:

char *month[] = {“January”, “February”, “March”, “April”, “May”,

“June”, “July”, “August”, “September”, “October”,

“November”, “December”};

create an ARMv8 assembly language program to accept as command line arguments three strings representing a date in the format <em>mm dd yyyy</em>. Your program will print the date with the name of month as well as the correct suffix. For example:

./a5b 9 11 1990

September 11th, 1990

Be sure to use the proper suffix for the day of the month. For example, one should distinguish the 11th from the 1st, 21st, and 31st. Don’t forget the comma after the day. Your program should exit, printing this error message, if the user does not supply three command-line arguments:

usage: a5b mm dd yyyy

You will need to call atoi() to convert strings to numbers, and printf() to produce the output. Be sure to do range checking for the day, month, and year. Name your source code file <em>a5b.asm</em>. Run your program three times with different input to illustrate that it works; capture the output using the <em>script </em>UNIX command. Name the output file <em>script2.txt</em>.

<strong>New Skills need for this Assignment:</strong>

<ul>

 <li>Understanding and use of external variables in assembly</li>

 <li>Separate compilation</li>

 <li>Calling assembly functions from main()</li>

 <li>Calling library functions from assembly routines</li>

 <li>External arrays of pointers</li>

 <li>Command line arguments</li>

</ul>




<strong> </strong>