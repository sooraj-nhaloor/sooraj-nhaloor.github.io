+++

title = "BibEditor "
date = "2023-10-16"
author = "Sooraj Nhaloor"

+++


  <span>

If you're a LaTeX user who's tired of the hassle that comes with managing lengthy lists of authors in your bibliography, then you're in the right place. 
In this post, I'm excited to introduce you to BibEditor, a handy tool that will make your life easier when dealing with the authors in LaTeX bibliographies.                            

BibEditor is my little experiment to limit the number of authors in the given .bib file.
Motivation for the program is nothing but I found that when adding bibliography in LaTeX
simply by using ```\bibliography``` will display all the authors, and I felt it is a pain-in-ass 
to manually edit each line of authors in a .bib file.

This program will ask you for the number of authors you want to display and remove all other
authors and put an et.al at the tail. Simple.

##   HOW TO USE

1) Place your ref.bib file in the same folder.

      [*Rename it to "ref.bib" (without quotations) if your .bib file has a different name.*] 	

2) Copy code, comple and run the program. You can use  [Geany](https://www.geany.org/).


3) The program will ask you for the number of maximum authors. Give what it asks! 

3) Press ENTER.	

4) Your modified .bib will be generated as output.bib

5) Verify for errors.

The source code of the program is given below . Feel free to make changes :)
### SOURCE CODE

```C




#include <stdio.h>
#include <string.h>
int maxauth;
char *inputf = "ref.bib";      
char *outputf = "output.bib";  
FILE *inputFile, *outputFile;
char copyLine[565];
char line[512];

int main() {

 printf("\n");
    printf("                          Welcome to BibEditor                                \n");
    printf("\n\n");

    printf("BibEditor is an experimental program to limit the number of authors in the given .bib file.\n");
    printf("Motivation for the program is nothing but I found that when adding bibliography in LaTeX\n");
    printf("simply by using \\bibliography will display all the authors, and I felt it is pain-in-ass \n");
    printf("to manually edit each line of authors in a .bib file.\n\n");

    printf("This program will ask you for the number of authors you want to display and simply remove all other\n");
    printf("authors and put an et.al at the tail. Simple :)\n\n");

    printf("¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯\n");
    printf("        HOW TO USE\n");
    printf("¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯\n\n");

    printf("1) Place your ref.bib file in the same folder.\n\n");

    
    printf("IMPORTANT: [ Rename it to \"ref.bib\" (without quotations) if .bib file has a different name. ]\n\n");

    printf("2) Run the program it will ask you for the number of maximum authors. Give what it asks! \n\n");

    printf("3) Press ENTER, and take a few deep breaths ;)\n\n");

    printf("4) Your modified .bib will be generated as output.bib\n\n");

    printf("5) Verify for errors.\n\n");

    printf("6) If you have any questions or need assistance:\n\n");

    printf("   Contact Information:\n");
    printf("   - Author: SOORAJ NHALOOR\n");
    printf("   - Email: soorajnhaloor123@gmail.com\n");
    printf("   - Website: sooraj-nhaloor.github.io\n\n");

    printf("════════════════════════════════════════════════════════════════════════════════\n");
    printf("\n\n");
    printf("\n\n");
    printf("Enter the number of maximum authors : ");
    scanf( "%d",&maxauth);
     printf("\n\n");
    printf("\n\n");
     printf("==============================================================================\n");
     printf("======================  DONT PANIC - LOGS  ===================================\n");
     printf("==============================================================================\n\n");
    inputFile = fopen(inputf, "r");    
    outputFile = fopen(outputf, "w");  

    if (inputFile == NULL || outputFile == NULL) {
        printf("Error opening files. Please read Readme.txt or see above ^\n");
        return 1;
    } else {
        char pattern[] = "author = {"; 
        while (fgets(line, sizeof(line), inputFile)) {
            if (strstr(line, pattern) != NULL) {
                printf("Pattern found in line: %s", line);
                int commaCount = 0;
                for (int i = 0; i < strlen(line); i++) {
                    if (line[i] == ',') {
                        commaCount++;
                        if (commaCount >= maxauth) {
                            copyLine[i] = line[i];
                        line[i] = '\0';


                            fprintf(outputFile, "%s %s et.al}\n",line,copyLine); 
                            break;
                        } /////////////////
                      
                    }
                }
                if (commaCount < maxauth) {
                    fprintf(outputFile,"%s",line);
                }
            } else {
                fprintf(outputFile, "%s", line); 
            }
        }

        fclose(inputFile);
        fclose(outputFile);
    }

    return 0;
}

```
