#include <stdio.h>
#include <stdlib.h>
 

void appendFiles(char src[], char dest[])
{
    FILE *ffp, *sfp;
 
    ffp = fopen(src, "a+");
    sfp = fopen(dest, "a+");
 
    if (!ffp && !sfp) {
        printf("Unable to open/" "detect file(s)\n");
        return;
    }
 
    char buf[500];
 
    fprintf(sfp, "\n");
 
    while (!feof(ffp)) {
        fgets(buf, sizeof(buf), ffp);
        fprintf(sfp, "%s", buf);
    }
 
    rewind(sfp);
 
    while (!feof(sfp)) {
        fgets(buf, sizeof(buf), sfp);
        printf("%s", buf);
    }
}
 

int main(int argc, char* argv[argc + 1])
{
    char src[] = "file.wat", dest[] = "count.c";
 
    appendFiles(src, dest);
 
    return EXIT_SUCCESS;
}
