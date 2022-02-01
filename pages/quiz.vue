<template>
  <article class="container">
    <section class="quiz align-items-center">
      <div class="alert alert-success" role="alert" v-show="end">
        Good Work Your Result is {{ mark }}
      </div>
      <div class="text-center">
        <h2>
          Quiz : <span class="orinage">{{ qNumber + 1 }}</span>
        </h2>
        <hr />
      </div>
      <div>
        <div class="q"><span class="orinage">Q:</span> {{ q }}</div>

        <ul class="list-group mt-2 px-2">
          <li id="a" class="list-group-item" @click="answer('a')">
            <span class="answer text-center">A</span> {{ a }}
          </li>
          <li id="b" class="list-group-item" @click="answer('b')">
            <span class="answer text-center">B</span> {{ b }}
          </li>
          <li
            v-show="c !== ''"
            id="c"
            class="list-group-item"
            @click="answer('c')"
          >
            <span class="answer text-center">C</span>{{ c }}
          </li>
          <li
            v-show="d !== ''"
            id="d"
            class="list-group-item"
            @click="answer('d')"
          >
            <span class="answer text-center">D</span>{{ d }}
          </li>
        </ul>
      </div>
      <button
        type="button"
        class="btn btn-success text-center btn-block"
        :disabled="choose || value == 'null'"
        @click="submit()"
      >
        Submit
      </button>
      <button
        type="button"
        class="btn btn-custom text-center btn-block"
        :disabled="choose == false"
        @click="next()"
      >
        Next
      </button>
    </section>
  </article>
</template>

<script>
export default {
  data() {
    return {
      choose: false,
      value: 'null',
      Questions: [
        {
          q: 'A mathematical statement is a combination of functions and variables only.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: ' In the function vpa(‘981’,10), why do we put 981 within inverted commas?',
          a: ' We can choose to not put the value within a pair of single inverted comma',
          b: 'We do it so that we don’t get an approximated value',
          c: 'We do it to get the exact value as MATLAB computes exact values, of numerical expressions, when declared within a string',
          d: ' We do it to get a floating-point approximated value, approximated to 14 digits',
          Answer: 'c',
        },
        {
          q: 'What are mathematical expressions?',
          a: ' Any mathematical relation',
          b: 'Any mathematical operation',
          c: 'Any mathematical conversation',
          d: 'Any mathematical function',
          Answer: 'b',
        },
        {
          q: 'How do you show the program of an MAT file?',
          a: 'The program should contain the echo command',
          b: 'The program should contain the showprog command',
          c: 'The program should contain the diary command',
          d: 'The program cannot be shown while running a MEX file',
          Answer: 'd',
        },
        {
          q: ' What will be the output of the following code? z:2+3i/(i99)',
          a: ' z conjugate',
          b: '-z',
          c: '-3+(2*i)',
          d: '-1',
          Answer: 'd',
        },
        {
          q: 'What will be the output of the following code? abs(i)',
          a: '1',
          b: '-1',
          c: 'Error',
          d: 'i',
          Answer: 'a',
        },
        {
          q: 'clc in a function will clear the function.',
          a: ' True',
          b: ' False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'Clear will removes all graphs.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },

        {
          q: ' What is a linear system?',
          a: 'A system which follows homogeneity and additivity',
          b: ' A system which follows additivity',
          c: 'A system which follows homogeneity',
          d: ' Almost every system is linear',
          Answer: 'a',
        },

        {
          q: ' To apply Cramer’s rule, the condition is _________',
          a: 'Non-homogeneous system of equations',
          b: 'Homogeneous system of equations',
          c: 'Determinant of co-efficient matrix is not equal to 0',
          d: 'No condition',
          Answer: 'c',
        },

        {
          q: 'To check the rank of a non-singular square matrix, we have to use _________',
          a: ' not required',
          b: ' rankm()',
          c: ' rankmatr()',
          d: 'rank()',
          Answer: 'd',
        },

        {
          q: ' Which rule does MATLAB use while differentiating a set of functions?',
          a: ' u-v rule',
          b: ' by parts',
          c: 'no pre-defined rule',
          d: 'not possible',
          Answer: 'a',
        },

        {
          q: 'For the existence of the nth (n is varying from 1 to until the derivative is becoming 0) derivative of an equation, the equation should have __________',
          a: ' Initial values',
          b: 'At least one independent variable',
          c: 'At least one dependent variable',
          d: 'No such condition',
          Answer: 'b',
        },

        {
          q: 'Graphs are not suppressed by the ‘;’.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },

        {
          q: ' There will be a problem in computing the logarithm of a negative number.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'The help command works only for a pre-defined function in MATLAB.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'a',
        },

        {
          q: 'What will be the output of the following code ? syms x;diff(sin(x)\\x2)',
          a: '(2*x)/sin(x) – (x2*cos(x))/sin(x)2',
          b: ' cos(x)/x2 – (2*sin(x))/x3',
          c: ' x2*cos(x) + 2*x*sin(x)',
          d: ' Error',
          Answer: 'a',
        },
        {
          q: ' Ordinary differential equations having initial values ____________',
          a: 'Can be solved',
          b: 'Cannot be solved',
          c: 'Can be modelled',
          d: 'Has a trivial solution',
          Answer: 'c',
        },

        {
          q: 'How would you express a pi as a character and an integer? Choose the correct code.',
          a: 'a:pi;b:’pi’;',
          b: 'a:22/7; b:pi;',
          c: 'a:3.1415; b:22/7;',
          d: 'a:3.1429;b:’pi’;',
          Answer: 'a',
        },

        {
          q: ' What is the output of the following code? A:[1 2 3]; A^2;',
          a: '[1 4 9]',
          b: ' A: 1 4 9',
          c: ' A: [1, 4, 9]',
          d: ' Inputs must be a scalar or a square matrix',
          Answer: 'd',
        },
        {
          q: 'What is the output of the following code? A:[1 1; 1 1]; A^2',
          a: ' A : 2 2 \n 2 2',
          b: ' A : 1 1 \n n 1 1',
          c: 'Error using ^ To compute element wise POWER, use POWER (.^) instead',
          d: ' No output',
          Answer: 'a',
        },
        {
          q: 'MEX files work on JAVA.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'Variables need to have same name while being passed from the primary function to the sub-function.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'If the dimensions of vectors don’t match, the plot command will always give an error.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'What is the difference between the two codes? \n a> P:[91,’pi’]; \n b> Q:[91,pi];',
          a: ' Code a initialises P as a character array while code b initialises Q as an integer array',
          b: ' Both P and Q will be integer arrays',
          c: ' Code b initialises P as a character array while code a initialises Q as an integer array',
          d: 'Both P and Q will be character arrays',
          Answer: 'a',
        },
        {
          q: 'What is the output of the following code? system(cmd)',
          a: ' Opens command prompt',
          b: ' Opens command prompt in a separate window',
          c: ' Opens command prompt in MATLAB',
          d: ' Error',
          Answer: 'd',
        },
        {
          q: " What is the output of the following code? clipboard('cut','Do re Mi fa')",
          a: ' Error due to syntax',
          b: 'Error due to command',
          c: 'Error due to cut',
          d: 'Cuts the portion of a text where ‘Do re Mi fa’ is written',
          Answer: 'c',
        },
        {
          q: 'What is the output of the following code? isvector((49 32));',
          a: 'Error in ()',
          b: ' Error due to absence of comma',
          c: ' Error due to command',
          d: ' Logical 1',
          Answer: 'a',
        },
        {
          q: ' What is the output of the following code? commandhistory[]',
          a: ' Error',
          b: ' Shows command history',
          c: ' Shows the previous command used',
          d: ' Prints all the commands used for the current session',
          Answer: 'a',
        },
        {
          q: "What is the output of the following code? p:input(''); po",
          a: ' ‘po’ gets assigned to p',
          b: ' Error in the input',
          c: ' Error due to syntax',
          d: ' Cannot be determined',
          Answer: 'b',
        },
        {
          q: 'Which function is preferable to find the magnitude of a complex number?',
          a: 'abs()',
          b: 'sqrt()',
          c: 'cart2pol()',
          d: 'MATLAB does not support complex arguments',
          Answer: 'a',
        },
        {
          q: ' All MATLAB computations are done in',
          a: 'Single Precision',
          b: 'Double Precision',
          c: 'Linear accuracy',
          d: 'Multi-level precision',
          Answer: 'b',
        },
        {
          q: ' Which symbol is used to initialise a variable?',
          a: ' :',
          b: '->',
          c: ' ::',
          d: 'init',
          Answer: 'a',
        },
        {
          q: 'What is the difference between the expressions (9*1-8) & (9-1*8)?',
          a: 'Computational difference',
          b: 'Final results are different',
          c: 'No difference',
          d: 'Cannot be determined',
          Answer: 'a',
        },
        {
          q: ' All matrices are vectors but all vectors are not matrices in MATLAB.',
          a: 'True',
          b: 'False',
          Answer: 'a',
        },
        {
          q: 'Matrix operations follow the rules of linear algebra and are not compatible with multidimensional arrays.',
          a: 'true',
          b: 'false',
          Answer: 'a',
        },
        {
          q: ' What is the output of the expression (2*9*Inf)+(9-1*Inf) ',
          a: 'Inf',
          b: 'Error',
          c: 'Incomprehensible',
          d: 'NaN',
          Answer: 'd',
        },
        {
          q: ' How many errors will MATLAB show if the following code entered? \n A:[1;2;3]; B:[1 2]; C:A.*B;D:C*A;',
          a: '2',
          b: '1',
          c: 'No error',
          d: '4',
          Answer: 'b',
        },
        {
          q: 'To see the sub-matrix with aij for 2<:i<:4 and 1<:j<:2 of a matrix a, of order 5*6, which code is used?',
          a: ' a(2;4,1;2)',
          b: ' a(2,4:1,2)',
          c: ' a(2:4,1:2)',
          d: ' a(2,4;1,2)',
          Answer: 'c',
        },
        {
          q: 'What is the symbol used to evaluate the transpose of a vector?',
          a: '“ ^ ”',
          b: '“ * ”',
          c: '“ ‘ ”',
          d: '“ ~ ”',
          Answer: 'c',
        },

        {
          q: ' Which code can be used for changing the dimensions of a matrix as follows? \n Input matrix: 1     2     3	\n	Output matrix: 1 4 2 5 3 6 \n 4     5     6',
          a: 'reshape([1,2,3;4,5,6],1,6)',
          b: 'reshape([1,2,3;4,5,6];1;6)',
          c: 'reshape([1,2,3;4,5,6]:1:6)',
          d: 'reshape([1,2,3;4,5,6],6,1)',
          Answer: 'a',
        },

        {
          q: 'Largest and smallest values for integer classes is 127 to -128.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'a',
        },
        {
          q: 'What is the function used to multiply a matrix, A, with itself n times?',
          a: 'mtimes(A,n)',
          b: 'ntimes(A,n)',
          c: 'mtimes(n,A)',
          d: 'mtimes(A^n)',
          Answer: 'a',
        },
        {
          q: 'If a./b:(b./a)T, what can be concluded about the matrices a and b?',
          a: 'a : bT',
          b: 'a : b-1',
          c: 'a : b’',
          d: 'nothing special',
          Answer: 'a',
        },
        {
          q: 'Choose the function to solve the following problem, symbolically, in the easiest way. 3x+y:5 and 2x+3y:7',
          a: 'linsolve(x,y) where x and y are the co-efficient and result matrix respectively',
          b: 'solve(x,y) where x and y are the co-efficient and result matrix respectively',
          c: 'sol(x,y) where x and y are the co-efficient and result matrix respectively',
          d: 'the equations are not solvable',
          Answer: 'a',
        },
        {
          q: ' What is the output of the following code? \n A:[1 2 3.. \n];',
          a: 'The output is suppressed',
          b: 'A row vector',
          c: 'A row vector concatenated with a null matrix',
          d: 'Error',
          Answer: 'd',
        },
        {
          q: 'Command is used to save command window text to file.',
          a: 'saveas',
          b: 'texttofile',
          c: 'diary',
          d: 'todiary',
          Answer: 'c',
        },
        {
          q: ' What is the output of the following code? ismatrix([]);',
          a: 'logical 1',
          b: 'logical 0',
          c: 'logical -1',
          d: 'Error',
          Answer: 'a',
        },
        {
          q: ' What is the output of the following code? \n A:[1 2 ‘a’…; \n ‘a’ ‘b’ ‘c’;… \n           ];',
          a: 'Error in syntax',
          b: 'A 3*2 matrix of characters',
          c: 'Error due to 1 and 2',
          d: 'Error due to a',
          Answer: 'a',
        },
        {
          q: "Round each value in a duration array to the nearest number of seconds greater than or equal to that value. \n t : hours(8) + minutes(29:31) + seconds(1.23); \n t.Format : 'hh:mm:ss.SS' \nt : 08:29:01.23   08:30:01.23   08:31:01.23 \n Y1 : ceil(t) Y2 : ceil(t,'hours') ",
          a: ' Y1 :  08:29:02.00   08:30:02.00   08:31:02.00  \n Y2 :  09:00:00.00   09:00:00.00   09:00:00.00  ',
          b:
            ' Y1 :  08:29:02.00   08:30:02.00   08:31:02.00 ' +
            ' Y2 :  08:29:01.23   08:30:01.23   08:31:01.23 ',
          c:
            ' Y1 :  08:29:01.23   08:30:01.23   08:31:01.23 ' +
            ' Y2 :  08:29:01.23   08:30:01.23   08:31:01.23 ',
          d:
            '  Y1 :  008:29:01.23   08:30:01.23   08:31:01.23' +
            'Y2 :  09:00:00.00   09:00:00.00   09:00:00.00    ',
          Answer: 'a',
        },
        {
          q: 'Compute 24 modulo 5. b : mod(24,5)',
          a: 'b : 3',
          b: 'b :4',
          c: 'b :5',
          d: 'b :6',
          Answer: 'b',
        },
        {
          q: 'What would be the output of the following code (in editor window)? X : [1 2 3;4 5 6;7 8 9]; Y : [9 8 7;6 5 4;3 2 1]; R : rem(X,Y)  ',
          a: 'R : 1     2     1 ; 4     0     9; 1     0     0  ;  ',
          b: ' R : 1     2     3 ; 3     0     2 ; 1     0     0  ; ',
          c: ' R : 1     2     3 ; 4     1     2 ;  1     1     0  ;   ',
          d: ' R : 1     2     3;4     0     2;1     0     0 ;    ',
          Answer: 'd',
        },
        {
          q: ' The expression cos(90) is equal to1 in MATLAB.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: ' If a character input is given to a command which only takes integers, it’ll always give an error.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'a',
        },
        {
          q: 'The uniform distribution can range from -infinity to 0 or 0 to Infinity but not from -infinity to infinity.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'MATLAB stands for?',
          a: 'matrix laboratory',
          b: 'math library',
          c: 'matric library',
          d: 'matrix library',
          Answer: 'a',
        },

        {
          q: 'Which command is used to clear a command window?',
          a: 'clear',
          b: 'close all',
          c: 'clc',
          d: 'clear all',
          Answer: 'c',
        },
        {
          q: 'Command used to display the value of variable x.',
          a: 'display',
          b: 'disp(x)',
          c: 'disp x',
          d: 'vardisp("x")',
          Answer: 'b',
        },

        {
          q: 'Executing in the command window the following code returns. a : [1:3] ; size(a)',
          a: 'error message',
          b: '1 3',
          c: '3 1',
          d: '31',
          Answer: 'c',
        },
        {
          q: 'Which is the invalid variable name in MATLAB?',
          a: 'x6',
          b: 'last',
          c: '6x',
          d: 'z',
          Answer: 'c',
        },
        {
          q: 'What would be the output of the following code (in editor window)? A : [0 1; 1 0]	;	B:2	;	C : A + B',
          a: '1	2; 4	5',
          b: '2	3 ; 3	2',
          c: ' 3	2; 3	2',
          d: ' 3	2 ;2	3',
          Answer: 'b',
        },
        {
          q: 'What would be the output of the following code (in editor window)? a:1:5	;	c:a.^2',
          a: '[1 25]',
          b: '[1 2 3 4 5]',
          c: '[25 16 9 4 1]',
          d: '[1 4 9 16 25]',
          Answer: 'd',
        },
        {
          q: 'Create an array of logical values. A = [true false true; true true false], A = 1     0     1 ; 1     1     0,B = cumprod(A,2), Find the cumulative product of the rows of A.',
          a: 'B = 1     0     0 ; 0     1     0',
          b: ' B = 1     0     0 ;1     1     0',
          c: 'B = 1     0     0 ;1     1     1',
          d: 'B = 1     1     0; 1     1     0',
          Answer: 'b',
        },
        {
          q: 'Find the cumulative sum of the columns of A. A  = 1     4     7; 2     5     8; 3     6     9 ; B = cumsum(A)',
          a: 'B = 1     4     7 ; 3     8    15 ; 6    15    24',
          b: ' B = 1     4     7;4     9    15;4    15    24',
          c: 'B = 1     4     7;3     9    15 ;6    15    29',
          d: 'B = 1     4     7 ;3     9    15;6    15    24',
          Answer: 'd',
        },
        {
          q: 'Create a 4-by-2-by-3 array of ones and compute the sum along the third dimension. A = ones(4,2,3); S = sum(A,3)',
          a: ' S = 3     3;3     3 ;3     3 ;3     3',
          b: 'S = 3     4 ; 3     4 ; 3     4  ;3     4',
          c: 'S = 2     3; 2     3; 2     3; 2     3',
          d: 'S = 7     3;5     3;6     3;3     3',
          Answer: 'a',
        },
        {
          q: 'Global variables must be mentioned _____ an M-file.',
          a: 'at the top in',
          b: 'anywhere in',
          c: 'out of the',
          d: 'there is nothing called global variables',
          Answer: 'a',
        },
        {
          q: 'What will be the output of the following code? T:-5:1:5; y:sin(T); plot(T,y)',
          a: 'No output',
          b: 'A perfect sine curve',
          c: 'A broken sine curve',
          d: 'Cannot be determined',
          Answer: 'c',
        },
        {
          q: 'The plotting of 3d plots and 2d plots requires separate windows. But the user has entered the hold on command. What is to be done?',
          a: 'Use the pause command',
          b: 'Use the hold off command',
          c: 'Use the close command',
          d: 'Nothing can be done',
          Answer: 'a',
        },

        {
          q: 'How will you return to execution from debugging mode?',
          a: 'Use the dbcont command',
          b: 'Use the return command',
          c: 'Use the dbcont & return command',
          d: 'Use the keyboard command',
          Answer: 'c',
        },
        {
          q: 'How will one escape from printing graphs of variables, whose value gets changed for the program?',
          a: 'Use the clear all command at the beginning',
          b: 'Use the close all command at the beginning',
          c: 'Use the clc command',
          d: 'Cannot be escaped',
          Answer: 'a',
        },
        {
          q: 'A loop is used to avoid repetitive writing of the same function in the code.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'a',
        },

        {
          q: 'The function to plot a graph with both axes on logarithmic scales is __________',
          a: 'loglog',
          b: 'log',
          c: 'semilog',
          d: 'not possible',
          Answer: 'a',
        },
        {
          q: 'The command used to reflect the files from a disk into the workspace is _______',
          a: 'load',
          b: 'show',
          c: 'disp()',
          d: 'it is not possible',
          Answer: 'a',
        },
        {
          q: 'How do you show the program of an MAT file?',
          a: 'The program should contain the echo command',
          b: 'The program should contain the showprog command',
          c: 'The program should contain the diary command',
          d: 'The program cannot be shown while running a MEX file',
          Answer: 'd',
        },
        {
          q: 'How would you plot multiple graphs in MATLAB?',
          a: 'Using the hold function',
          b: 'Using the mplot function',
          c: 'Using the mstem function',
          d: 'It cannot be done in MATLAB',
          Answer: 'a',
        },
        {
          q: 'We cannot plot a discrete and continuous relationship in the same graph.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'It is not possible to store graphs as MAT-file.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'a',
        },

        {
          q: 'What is the nature of the following code? j:0;i:1; while(j>5) \n for i:1:8 \nj:j+i; endend',
          a: 'j:0 & i:1',
          b: 'j:1 & i:0',
          c: 'i:8 & j:36',
          d: 'Error',
          Answer: 'a',
        },
        {
          q: 'Which functions help you to save and load variables?',
          a: ' >> save Lays [a,b] \n, >> load("myfile.mat")',
          b: '>> save Lays {a b} , \n >> load myfile.mat',
          c: " >> save Lays 'a,b' \n ,>> load(myfile.mat)",
          d: '>> save Lays a b \n >> load("myfile.mat")',
          Answer: 'd',
        },
        {
          q: 'To add comments in MATLAB, use _________',
          a: '//',
          b: '%/',
          c: '/%',
          d: '%',
          Answer: 'd',
        },
        {
          q: 'There can be multiple decision variables for while loop.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'a',
        },
        {
          q: 'A break statement will leave the outer loop.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'To display comments of M-file, we use ____________',
          a: 'echo on',
          b: 'comment on',
          c: 'show %',
          d: 'Cannot be displayed',
          Answer: 'a',
        },
        {
          q: "What will the following set of commands do when they are present in a script file? stem[y1,y2]; title('p'); print -deps p",
          a: 'Plot the discrete graph of y1 and y2',
          b: 'There is no stem command in MATLAB',
          c: 'Store the graph as a separate file',
          d: 'Cannot be determined',
          Answer: 'c',
        },
        {
          q: 'The function to close the windows containing graphs generated from MATLAB is __________',
          a: 'close all',
          b: 'close graphs',
          c: 'delete graphs',
          d: 'end all',
          Answer: 'a',
        },
        {
          q: 'MATLAB allows modelling of different control systems using ___________',
          a: 'Simulink',
          b: 'Control System Toolbox',
          c: 'Not available in MATLAB as of yet',
          d: 'ezplot',
          Answer: 'a',
        },
        {
          q: 'A second order system with no initial condition is always linear.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'a',
        },
        {
          q: 'The current characteristics of RC networks are better analyzed by Laplace than differentiation methods.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'How would you start a debugger in MATLAB?',
          a: 'There is no M-file in MATLAB',
          b: 'Type edit in MATLAB and press Enter',
          c: 'Type debug in MATLAB and press Enter',
          d: 'Type M-file in MATLAB and press Enter',
          Answer: 'b',
        },
        {
          q: 'What does the echo command do?',
          a: 'It echoes',
          b: 'It shows the comments present in Script files',
          c: 'It shows the commands and comments in MAT-files',
          d: 'It shows the commands and the comments in M-files',
          Answer: 'd',
        },
        {
          q: 'What will the following command do? Save workspace',
          A: 'Saves the entire workspace as MAT file',
          b: "Saves a variable named'workspace' as MAT file",
          c: 'Saves the entire workspace as m file',
          d: "Saves a variable named 'workspace' as m file",
          Answer: 'b',
        },
        {
          q: 'What is the syntax to solve simultaneous equations easily?',
          a: "solve['equation-1','equation-2'];",
          b: "sol['equation-1' 'equation-2'];",
          c: "sol['equation-1''equation-2'];",
          d: "solve['equation-1','equation-2'];",
          Answer: 'd',
        },
        {
          q: "Vectors depend upon brackets while scalars don't.",
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'a',
        },
        {
          q: "What should be the output for the following code? t:linspace(0,10);fzero(inline('t+t2'), 5);",
          a: 'Nan',
          b: '-0.000000000000000000000000117191203927370461282452866337',
          c: '-1.1719e-25',
          d: 'fzero is not a function',
          Answer: 'a',
        },
        {
          q: 'A student has to find the solution of an equation cos(x):1/2. She has to write the program such that exact values are shown at output. Which of the following codes would help her?',
          a: 'syms x;eqn : cos(x) :: 1/2;vpa( solve(eqn,x))',
          b: 'syms x;eqn : cos(x) :: 1/2;solve(eqn,x)',
          c: "vpa(solve('cos(x):1/2'))",
          d: 'syms x;eqn : cos(x) : 1/2;vpa(solve(eqn,x))',
          Answer: 'c',
        },
        {
          q: 'Name the functions used, for multiplication and division of two polynomials in MATLAB.',
          a: 'conv() and deconv()',
          b: 'mult() and div()',
          c: 'conv() and div()',
          d: 'mult and div',
          Answer: 'a',
        },
        {
          q: 'What will be the output for the below block of code? P:[1 3 2]; r:roots(P);',
          a: 'r:[-2,-2]',
          b: 'r:[-2 -1]',
          c: 'There is an error in the code',
          d: 'r : -2 ;-1',
          Answer: 'd',
        },
        {
          q: "What happens if we don't assign a variable to an expression which evaluates a numerical value?",
          a: 'MATLAB shows error',
          b: 'Nothing happens',
          c: 'The evaluated values are assigned to a variable ans automatically',
          d: 'Depends on the numerical value',
          Answer: 'c',
        },
        {
          q: 'There is no difference between a difference equation and a differential equation.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'The modulus of z, z conjugate and -z are not equal in MATLAB.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
        {
          q: 'A mathematical statement is a combination of functions and variables only.',
          a: 'True',
          b: 'False',
          c: '',
          d: '',
          Answer: 'b',
        },
      ],
      q: '',
      a: '',
      b: '',
      c: '',
      d: '',
      result: '',
      mark: null,
      qNumber: 0,
      end: false,
    }
  },
  mounted() {
    const q1 = this.Questions[this.qNumber]
    this.q = q1.q
    this.a = q1.a
    this.b = q1.b
    this.c = q1.c
    this.d = q1.d
    this.result = q1.Answer
  },
  methods: {
    answer(id) {
      const ele = document.querySelectorAll('.list-group-item')

      ele.forEach((element) => {
        element.classList.remove('active')
      })

      document.getElementById(id).classList.add('active')
      this.value = `${id}`
    },
    submit() {
      this.choose = true

      if (this.value === this.result) {
        document.getElementById(this.value).classList.remove('active')
        document.getElementById(this.value).classList.add('true')
        this.mark = this.mark + 1
      } else {
        document.getElementById(this.value).classList.remove('active')
        document.getElementById(this.result).classList.add('true')
        document.getElementById(this.value).classList.add('false')
      }
    },
    next() {
      this.choose = false
      document.getElementById(this.value).classList.remove('active')
      document.getElementById(this.result).classList.remove('true')
      document.getElementById(this.value).classList.remove('false')
      this.qNumber++
      this.value = 'null'

      if (this.qNumber >= this.Questions.length) {
        this.$router.push(`/result/${this.mark}`)
        return
      }
      const q1 = this.Questions[this.qNumber]
      this.q = q1.q
      this.a = q1.a
      this.b = q1.b
      this.c = q1.c
      this.d = q1.d
      this.result = q1.Answer
    },
  },
}
</script>
<style lang="scss">
$color1: #1f2639;
$color2: #e78231;
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
  scroll-behavior: smooth;
  background-color: $color1;
}
.container {
  display: flex;
  justify-content: center;
  position: relative;
}

section {
  border: 2px solid rgb(49, 40, 40);
  min-width: 80%;
}
.quiz {
  padding: 10px;
  color: white;
  .orinage {
    color: $color2;
  }
  .q {
    font-size: 20px;
  }

  .list-group-item {
    background-color: #e8e8ea;
    color: black;
    border-radius: 20px;
    margin-bottom: 5px;

    &:hover {
      outline: 1px solid $color2;
      border-radius: 20px;
    }
  }
  .active {
    background-color: $color2;
    border: none;
    margin-top: 0;
    transition: 0.5s ease-in-out;
  }

  .true {
    background-color: green;
    border: none;
    margin-top: 0;
  }

  .false {
    background-color: red;
    border: none;
    margin-top: 0;
  }
  .answer {
    border-radius: 50%;
    border: 1px solid;
    background-color: $color2;
    color: white;
    padding: 6px;
    margin-right: 10px;
    box-shadow: 2px silver;
  }

  .btn-custom {
    color: #fff;
    background-color: $color2;
    border-color: $color2;
    &:focus {
      color: #fff;
      background-color: $color2;
      border-color: $color2;
      box-shadow: 0 0 0 0.2rem #dc7827;
    }
    &:hover {
      background-color: #c65a04;
    }
  }
}
</style>
