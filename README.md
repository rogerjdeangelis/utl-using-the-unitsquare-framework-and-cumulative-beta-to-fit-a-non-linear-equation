# utl-using-the-unitsquare-framework-and-cumulative-beta-to-fit-a-non-linear-equation
Using the unitsquare framework and cumulative beta to fit a nin linear equation
    %let pgm=utl-using-the-unitsquare-framework-and-cumulative-beta-to-fit-a-non-linear-equation;

    Using the unitsquare framework and cumulative beta to fit a nin linear equation
                           _     _
      __ _ _ __ __ _ _ __ | |__ (_) ___
     / _` | `__/ _` | `_ \| `_ \| |/ __|
    | (_| | | | (_| | |_) | | | | | (__
     \__, |_|  \__,_| .__/|_| |_|_|\___|
     |___/          |_|

    output
    https://tinyurl.com/2vrutwfe
    https://github.com/rogerjdeangelis/utl-using-the-unitsquare-framework-and-cumulative-beta-to-fit-a-non-linear-equation/blob/main/pltgrf.pdf


    github
    https://tinyurl.com/ypkphd6t
    https://github.com/rogerjdeangelis/utl-using-the-unitsquare-framework-and-cumulative-beta-to-fit-a-non-linear-equation

    Improving the stackoverflow fit

            SOLUTIONS
               1 stackoverflow solution
               2 unit square
               3 both line plot
               4 hi res plot

    https://stackoverflow.com/questions/44183427/non-linear-fit-in-r

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                |                         |                                                             */
    /*           INPUT                |      PROCESS            |                      OUTPUT                                 */
    /*           =====                |      =======            |                      ======                                 */
    /*                                |                         |                                                             */
    /*          MAPPED TO UNIT SQUARE |                         |                IMPROVE STACKOVERFLOW FIT                    */
    /*                                | proc nlin data=sd1.have |                                                             */
    /*            TIME/14   CUM/1441  |    method=MARQUARDT     |                          TIME                               */
    /* TIME  CUM     XS        YS     |    CONVERGE=0.001;      |                                                             */
    /*                                |  parms A = 8            |         0  1  2  3  4  5  6  7  8  9 10 11 12 13 14         */
    /*   0     0  0.00000   0.00000   |        B = 5            | cum  ---+--+--+--+--+--+--+--+--+--+--+--+--+--+--+---      */
    /*   1    20  0.07143   0.01388   |        C = 1            |      |                                               |      */
    /*   2    45  0.14286   0.03123   |        ;                | 1500 + Finding a better fit than Stackoverflow       + 1500 */
    /*   3    99  0.21429   0.06870   |  model                  |      |                                               |      */
    /*   4   195  0.28571   0.13532   |   ys=                   |      |  * RAW DATA              exact fit roger  r*  |      */
    /*   5   301  0.35714   0.20888   |    CDF('BETA',xs,a,b)+  |      |  o STACKOVERFLOW                           |  |      */
    /*   6   407  0.42857   0.28244   |    c*sin(3.14*xs);      |      |  r ROGER              stackoverflow diff ->|  |      */
    /*   7   501  0.50000   0.34768   |  output                 |      |                                            |  |      */
    /*   8   582  0.57143   0.40389   |   out=unitsquare        | 1350 +  Unit Square Mean Square Errors            |  + 1350 */
    /*   9   679  0.64286   0.47120   |   p=predicted           |      |                                            |  |      */
    /*  10   753  0.71429   0.52255   |   r=residual;           |      |  stackoverflow 0.0570                      |  |      */
    /*  11   790  0.78571   0.54823   |                         |      |  roger         0.0146 * improvment         o  |      */
    /*  12   861  0.85714   0.59750   | Using the beta cdf      |      |                                               |      */
    /*  13  1011  0.92857   0.70160   | and/or sine/cosine      |      |                                               |      */
    /*  14  1441  1.00000   1.00000   | can force exact fits    | 1200 +                                               + 1200 */
    /*                                | at mins and maxes of    |      |                                               |      */
    /*                                | x and y.                |      |                                               |      */
    /*                                |                         |      |                                         o -    |     */
    /*                                |                         |      |                                           |   |      */
    /*                                |                         |      |                    stackoverflow diff  -->|   |      */
    /*                                |                         | 1050 +                                         r |   + 1050 */
    /*                                |                         |      |                               roger dif | |   |      */
    /*                                |                         |      |                                         * -   |      */
    /*                                |                         |     \\                                              \\      */
    /*                                |                         |     \\                                              \\      */
    /*                                |                         |     \\      ROUGHLY EQUAL PREDICTIONS IN HERE       \\      */
    /*                                |                         |     \\                                              \\      */
    /*                                |                         |     \\                                              \\      */
    /*                                |                         |  300 +                r*                             + 300  */
    /*                                |                         |      |                 o                             |      */
    /*                                |                         |      |              r                                |      */
    /*                                |                         |      |              o                                |      */
    /*                                |                         |      |              *       * RAW DATA               |      */
    /*                                |                         |      |           o          o STACKOVERFLOW          |      */
    /*                                |                         |  150 +           r          r ROGER                  + 150  */
    /*                                |                         |      |        o                                      |      */
    /*                                |                         |      |     o  r  * raw data                                  |      */
    /*                                |                         |      |  o                                            |      */
    /*                                |                         |      |     r  *                                      |      */
    /*                                |                         |      |     *                                         |      */
    /*                                |                         |    0 + r*  exact roger fit                           + 0    */
    /*                                |                         |      |                                               |      */
    /*                                |                         |      ---+--+--+--+--+--+--+--+--+--+--+--+--+--+--+---      */
    /*                                |                         |         0  1  2  3  4  5  6  7  8  9 10 11 12 13 14         */
    /*                                |                         |                                                             */
    /*                                |                         |                          TIME                               */
    /*                                |                         |                                                             */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */


    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
    input time cum ;
    xs=time/14;;
    ys=cum/1441;
    cards4;
    0 0
    01 20
    02 45
    03 99
    04 195
    05 301
    06 407
    07 501
    08 582
    09 679
    10 753
    11 790
    12 861
    13 1011
    14 1441
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   TIME     CUM       XS         YS                                                                                     */
    /*                                                                                                                        */
    /*     0        0    0.00000    0.00000                                                                                   */
    /*     1       20    0.07143    0.01388                                                                                   */
    /*     2       45    0.14286    0.03123                                                                                   */
    /*     3       99    0.21429    0.06870                                                                                   */
    /*     4      195    0.28571    0.13532                                                                                   */
    /*     5      301    0.35714    0.20888                                                                                   */
    /*     6      407    0.42857    0.28244                                                                                   */
    /*     7      501    0.50000    0.34768                                                                                   */
    /*     8      582    0.57143    0.40389                                                                                   */
    /*     9      679    0.64286    0.47120                                                                                   */
    /*    10      753    0.71429    0.52255                                                                                   */
    /*    11      790    0.78571    0.54823                                                                                   */
    /*    12      861    0.85714    0.59750                                                                                   */
    /*    13     1011    0.92857    0.70160                                                                                   */
    /*    14     1441    1.00000    1.00000                                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*       _             _                        __ _
    / |  ___| |_ __ _  ___| | _______   _____ _ __ / _| | _____      __
    | | / __| __/ _` |/ __| |/ / _ \ \ / / _ \ `__| |_| |/ _ \ \ /\ / /
    | | \__ \ || (_| | (__|   < (_) \ V /  __/ |  |  _| | (_) \ V  V /
    |_| |___/\__\__,_|\___|_|\_\___/ \_/ \___|_|  |_| |_|\___/ \_/\_/

    */

    ods trace on;
    ods output parameterestimates=est;
    proc nlin data=sd1.have method=MARQUARDT CONVERGE=0.001;
      parms A = 0.001
            B = 1000
            C = 0.5
            ;
      model ys = B/((B*C)*exp(-A*B*time) + 1) ;
      output out=stackoverflow p=predicted r=residual;
    run;quit;
    ods trace off;
                                      Sum of        Mean               Approx
    /*************************************************************************************************************************/*
    /*                                                                                                                        /*
    /*  Source                    DF     Squares      Square    F Value    Pr > F                                             /*
    /*                                                                                                                        /*
    /*  Model                      3      3.0233      1.0078     208.35    <.0001                                             /*
    /*  Error                     11      0.0532     0.00484                                                                  /*
    /*  Uncorrected Total         14      3.0765                                                                              /*
    /*                                                                                                                        /*
    /*                                                                                                                        /*
    /*                                Approx                                                                                  /*
    /*  Parameter      Estimate    Std Error    Approximate 95% Confidence Limits                                             /*
    /*                                                                                                                        /*
    /*  A                0.1240       0.1203     -0.1408      0.3888                                                          /*
    /*  B                1.8683       1.3125     -1.0204      4.7570                                                          /*
    /*  C               14.8735       5.6110      2.5239     27.2231                                                          /*
    /*                                                                                                                        /*
    /*************************************************************************************************************************/*

    options ls=64 ps=44;
    proc plot data= stackoverflow;
     plot ys*xs='*' predicted*xs='p'/overlay box haxis=0 to 1 by .2;
    run;quit;
    options ps=65 ls=171;

         0.0        0.2        0.4        0.6        0.8        1.0
        --+----------+----------+----------+----------+----------+--
     YS |                                                          |
        |                                                          |
    1.0 +                                                        * + 1.0
        |                                                          |
        |     o stackoverflow                                      |
        |     * raw data                                         o |
        |                                                          |
        |                                                          |
    0.8 +                                                    o     + 0.8
        |                                                          |
        |                                                          |
        |                                                o   *     |
        |                                                          |
        |                                                          |
    0.6 +                                            o   *         + 0.6
        |                                                          |
        |                                        *   *             |
        |                                        o                 |
        |                                    *                     |
        |                                    o                     |
    0.4 +                                *                         + 0.4
        |                                                          |
        |                             *  o                         |
        |                             o                            |
        |                         *                                |
        |                         o                                |
    0.2 +                     *                                    + 0.2
        |                                                          |
        |             o   *                                        |
        |         o                                                |
        | o   o       *                                            |
        |         *                                                |
    0.0 + *   *                                                    + 0.0
        |                                                          |
        --+----------+----------+----------+----------+----------+--
         0.0        0.2        0.4        0.6        0.8        1.0

                                     XS

    /*___
    |___ \   _ __ ___   __ _  ___ _ __
      __) | | `__/ _ \ / _` |/ _ \ `__|
     / __/  | | | (_) | (_| |  __/ |
    |_____| |_|  \___/ \__, |\___|_|
                       |___/
    */
    ods output parameterestimates=est;
    proc nlin data=sd1.have
        method=MARQUARDT
        CONVERGE=0.001;
      parms A = 8
            B = 5
            C = 1
            ;
      model
       ys=CDF('BETA',xs,a,b)+c*sin(3.14*xs);
      output
       out=unitsquare
       p=predicted
       r=residual;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  options ls=90 ps=44;                                                                                                  */
    /*  proc plot data= unitsquare;                                                                                           */
    /*   plot ys*xs='*' predicted*xs='p'/overlay box haxis=0 to 1 by .2;                                                      */
    /*  run;quit;                                                                                                             */
    /*  options ps=65 ls=171;                                                                                                 */
    /*                                                                                                                        */
    /*                                    Sum of        Mean               Approx                                             */
    /*  Source                    DF     Squares      Square    F Value    Pr > F                                             */
    /*                                                                                                                        */
    /*  Model                      3      3.0619      1.0206     770.68    <.0001                                             */
    /*  Error                     11      0.0146     0.00132                                                                  */
    /*  Uncorrected Total         14      3.0765                                                                              */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*                                Approx                                                                                  */
    /*  Parameter      Estimate    Std Error    Approximate 95% Confidence Limits                                             */
    /*                                                                                                                        */
    /*  A                1.3651       2.8683     -4.9480      7.6782                                                          */
    /*  B                0.5473       0.4220     -0.3816      1.4762                                                          */
    /*  C                0.0992       0.4311     -0.8497      1.0482                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/



    options ls=64 ps=44;
    proc plot data= unitsquare;
     plot ys*xs='*' predicted*xs='p'/overlay box haxis=0 to 1 by .2;
    run;quit;
    options ps=65 ls=171;

                                     xs
         0.0        0.2        0.4        0.6        0.8        1.0
        --+----------+----------+----------+----------+----------+-- ys
     YS |                                                          |
        |                                                          |
    1.0 +                                                       r* + 1.0
        |                                                          |
        |                                                          |
        |                                                          |
        |                                                          |
        |                                                          |
    0.8 +                                                          + 0.8
        |                                                          |
        |                                                    r     |
        |                                                    *     |
        |                                                          |
        |                                                r         |
    0.6 +                                                *         + 0.6
        |                                            r             |
        |                                        *   *             |
        |                                        r                 |
        |                                    *                     |
        |                                    r                     |
    0.4 +                                *                         + 0.4
        |                                r                         |
        |                            r*                            |
        |                                                          |
        |                        r*                                |
        |                     r                                    |
    0.2 +                     *                                    + 0.2
        |                 r                                        |
        |             r   *                                        |
        |                                                          |
        |         r   *                                            |
        |     r   *                                                |
    0.0 + r*  *                                                    + 0.0
        |                                                          |
        --+----------+----------+----------+----------+----------+--
         0.0        0.2        0.4        0.6        0.8        1.0

                                     XS
    /*____   _           _   _
    |___ /  | |__   ___ | |_| |__
      |_ \  | `_ \ / _ \| __| `_ \
     ___) | | |_) | (_) | |_| | | |
    |____/  |_.__/ \___/ \__|_| |_|

    */

    proc sql;
      create
         table check as
      select
         l.xs*14 as xs
        ,l.ys*1441 as ys
        ,l.predicted*1441 as stackoverflow
        ,r.predicted*1441 as roger
      from
         stackoverflow as l, unitsquare as r
      where
         l.xs = r.xs
    ;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  XS      YS    STACKOVERFLOW      ROGER                                                                                */
    /*                                                                                                                        */
    /*   0       0         84.14          0.00                                                                                */
    /*   1      20        106.90         51.41                                                                                */
    /*   2      45        135.44        113.55                                                                                */
    /*   3      99        171.02        180.72                                                                                */
    /*   4     195        215.01        250.61                                                                                */
    /*   5     301        268.88        321.85                                                                                */
    /*   6     407        334.10        393.79                                                                                */
    /*   7     501        411.94        466.43                                                                                */
    /*   8     582        503.28        540.49                                                                                */
    /*   9     679        608.35        617.60                                                                                */
    /*  10     753        726.52        700.62                                                                                */
    /*  11     790        856.04        794.38                                                                                */
    /*  12     861        994.10        907.72                                                                                */
    /*  13    1011       1136.94       1061.51                                                                                */
    /*  14    1441       1280.25       1441.23                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    options ls=80 ps=80;
    proc plot data= check(rename=ys=ys123456789012345678901234567);
     plot ys123456789012345678901234567*xs='*' stackoverflow*xs='o' roger*xs='r'/overlay box
      vaxis=0 to 1500 by 150;
    run;quit;
    options ps=65 ls=171;

             0  1  2  3  4  5  6  7  8  9 10 11 12 13 14
          ---+--+--+--+--+--+--+--+--+--+--+--+--+--+--+---
          |                                               |
          |                                               |
      1500 +                                               +
          |                                               |
          |                                    exact  r*  |
          |                                               |
          |                                               |
          |                                               |
      1350 +                                               +
          |                                               |
          |                                               |
          |                              stackoverflow o  |
          |                                               |
          |                                               |
      1200 +                                               +
          |                                               |
          |                                               |
          |                                         o     |
          |                                               |
          |                                               |
      1050 +                                         r     +
          |                                               |
          |                                      o  *     |
          |                                               |
          |                                               |
          |                                               |
      900 +                                      r        +
          |                                               |
          |                                   o  *        |
          |                                               |
          |                                   *           |
          |                                               |
      750 +                                *              +
          |                                o              |
          |                                r              |
          |                             *                 |
          |                                               |
          |                             r                 |
      600 +                             o                 +
          |                          *                    |
          |                          r                    |
          |                                               |
          |                       *  o                    |
          |                       r                       |
      450 +                                               +
          |                                               |
          |                    *  o                       |
          |                                               |
          |                                               |
          |                 r  o                          |
      300 +                 *                             +
          |                 o                             |
          |              r                                |
          |              o                                |
          |              *                                |
          |           o                                   |
      150 +           r                                   +
          |        o                                      |
          |     o  r  *                                   |
          |  o                                            |
          |     r  *                                      |
          |     *                                         |
        0 + r* exact                                      +
          |                                               |
          ---+--+--+--+--+--+--+--+--+--+--+--+--+--+--+---
             0  1  2  3  4  5  6  7  8  9 10 11 12 13 14

                               XS

    /*  _     _     _                             _       _
    | || |   | |__ (_)      _ __ ___  ___   _ __ | | ___ | |_
    | || |_  | `_ \| |_____| `__/ _ \/ __| | `_ \| |/ _ \| __|
    |__   _| | | | | |_____| | |  __/\__ \ | |_) | | (_) | |_
       |_|   |_| |_|_|     |_|  \___||___/ | .__/|_|\___/ \__|
                                           |_|
    */


    ods graphics on / width=10in height=7in;
    ods pdf file="d:/pdf/pltgrf.pdf" style=journal;

    title ;
    proc sgplot data=check;
    label  ys="Original"
           Stackoverflow="Stackoverflow"
           roger="Roger"
    ;
    series x=xs y=roger    / lineattrs=(thickness=1pt color=blue);
    series x=xs y=ys       / lineattrs=(thickness=1pt  color=green);
    series x=xs y=stackoverflow   / lineattrs=(thickness=1pt color=red);

    keylegend / location = inside position=left;

    run;quit;

    ods pdf close;

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
