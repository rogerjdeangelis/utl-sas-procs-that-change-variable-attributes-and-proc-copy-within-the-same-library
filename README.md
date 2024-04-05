# utl-sas-procs-that-change-variable-attributes-and-proc-copy-within-the-same-library
Sas procs that change variable attributes and proc copy within the same library
    %let pgm=utl-sas-procs-that-change-variable-attributes-and-proc-copy-within-the-same-library;

    Sas procs that change variable attributes and proc copy within the same library

    proc copy expects the input library be different from the output directory

    github
    https://tinyurl.com/5b39bhps
    https://github.com/rogerjdeangelis/utl-sas-procs-that-change-variable-attributes-and-proc-copy-within-the-same-library

       Examples

          1. proc sort & report Renove Attributes
             It is often disireable to remove attributes
             because some procs use them and others do not

          2. Proc sort change attributes

          3. proc copy input & output in same library
             Optionally can can also change attributes


    /*************************************************************************************************************************************/
    /*                                                    |                                          |                                   */
    /*                                                    |                                          |                                   */
    /*                  INPUT                             |                PROCESS                   |            OUTPUT                 */
    /*                  =====                             |                =======                   |            ======                 */
    /* data class;                                        |                                          |                                   */
    /* set sashelp.class(obs=3 keep=sex age);             | 1. REMOVE ATTRIBUTES(FROM OUTPUT)        | DataSet Name: WORK.CLASSSRT       */
    /* attrib                                             |                                          |                                   */
    /*  SEX  format=$1. informat=$2. label="Student Sex"  | proc sort data=class out=classSrt;       | Variable Type Len                 */
    /*  AGE  format=3.  informat=4.  label="Student Age"  | format _numeric_; format _character_;    |                                   */
    /* ;                                                  | informat _numeric_;informat _character_; | SEX      Char   1                 */
    /* run;quit;                                          | label age=;                              | AGE      Num    8                 */
    /*                     Remove these attributes        | label sex=;                              |                                   */
    /*                     =============================  | by sex;                                  |                                   */
    /* Variable Type  Len  Format  Informat  Label        | run;quit;                                |                                   */
    /*                                                    |                                          |                                   */
    /* AGE      Num     8  3.        4.      Student Age  |                                          |                                   */
    /* SEX      Char    1  $1.       $2.     Student Sex  |                                          |                                   */
    /*                                                    |                                          |                                   */
    /*----------------------------------------------------|------------------------------------------|-----------------------------------*/
    /*                                                    |                                          |                                   */
    /*                                                    | 2. CHANGE ATTRIBUTES (SORT)              | Variable Format Informat Label    */
    /*                      Remove these                  |                                          |                                   */
    /*                      ============================= | proc sort data=class out=classSrt;       | SEX      $32.     $99.   New Sex  */
    /*  Variable Type  Len  Format  Informat  Label       | format age best.; format sex $32.;       | AGE      BEST.    F9.    New Age  */
    /*                                                    | informat age 9.; informat sex $99.;      |                                   */
    /*  AGE      Num     8  3.        4.      Student Age | label age="New Age";                     |                                   */
    /*  SEX      Char    1  $1.       $2.     Student Sex | label sex="New Sex";                     |                                   */
    /*                                                    | by sex;                                  |  DataSet Name: WORK.CLASSSRT      */
    /*                                                    | run;quit;                                |                                   */
    /*                                                    |                                          |  Variable Type Len                */
    /*                                                    |    CHANGE ATTRIBUTES (REPORT)            |                                   */
    /*                                                    | proc report data=class out=classrpt;     |  SEX      Char   1                */
    /*                                                    | format _numeric_; format _character_;    |  AGE      Num    8                */
    /*                                                    | informat _numeric_;informat _character_; |                                   */
    /*                                                    | label age=;                              |                                   */
    /*                                                    | label sex=;                              |                                   */
    /*                                                    | run;quit;                                |                                   */
    /*                                                    |                                          |                                   */
    /*----------------------------------------------------|------------------------------------------|-----------------------------------*/
    /*                                                    |                                          |                                   */
    /*                                                    | 3. PROC COPY IN & OUT IN SAME LIBRARY    |                                   */
    /*                                                    |                                          |                                   */
    /*                                                    | proc datasets lib=work nodetails nolist; |     NAME           TYPE  OBS VARS */
    /*                                                    |   delete copy_in_same_library;           |                                   */
    /*                                                    | run;quit;                                | WORK.CLASS          DATA   3   2  */
    /*                                                    |                                          | WORK.COPY_IN_SAME_                */
    /*                       Remove these attributes      |  * INPUT AND OUTPUT IN WORK DIRECTORY;   |            LIBRARY  DATA   3   2  */
    /*                       ===========================  |                                          |                                   */
    /*   Variable Type  Len  Format Informat Label        | proc append base=copy_in_same_library    |                                   */
    /*                                                    |     data=class;                          |                                   */
    /*   AGE      Num     8  3.       4.     Student Age  | format _numeric_; format _character_;    |                                   */
    /*   SEX      Char    1  $1.      $2.    Student Sex  | informat _numeric_; informat _character_;|                                   */
    /*                                                    | label age=;                              |                                   */
    /*                                                    | label sex=;                              |                                   */
    /*                                                    | run;quit;                                |                                   */
    /*                                                    |                                          |                                   */
    /*************************************************************************************************************************************/

     /*             _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
