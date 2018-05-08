# utl_infinite_precision_and_why_iap_shoud_be_zero_but_is_not
Infinite Precision and why IAP shoud be zero but is not. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Infinite Precision and why IAP shoud be zero but is not

    github
    https://tinyurl.com/yc73pyro
    https://github.com/rogerjdeangelis/utl_infinite_precision_and_why_iap_shoud_be_zero_but_is_not

    see
    https://stackoverflow.com/questions/50225020/incorrect-floating-point-aggregation

    128bit floats would be nice?


      Three SOLUTIONS

        1. Greatly reduces the and close to infinite for many sums
        2. Infinite Precision Pennies: and sumis in pennies sum is exact
        3. Infinite Precision Dollars: Uses picture format to display sum in dollars with infinite precision
    *                _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | '_ \| '__/ _ \| '_ \| |/ _ \ '_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    ;

    data t;
    input a b $ c $ d ;
    *d=round(100*d);
    datalines;
    481710428888 24Nov2010 NP 34961.0000
    481710428888 07Mar2013 IP 175455.7500
    481710428888 09Nov2015 WB -63835.6400
    481710428888 23Nov2015 WO 27074.9000
    481710428888 23Nov2015 WO 49240.6500
    481710428888 23Nov2015 WO 70265.5600
    481910257067 01Apr2010 NP 47129.0000
    481910257067 27May2010 WO 47129.0000
    481910257067 22Mar2013 IP 3287.6900
    481910257067 11Apr2013 WO 3287.6900
    ;
    run;

    PROC SQL;
    SELECT DISTINCT
           put(a, z20.) AS ACCOUNT_NUMBER,
           b,
           c,
           d,
           (CASE WHEN c  = 'WO' THEN -1 ELSE 1 END) * d AS PRVN_A
            ,SUM (CALCULATED PRVN_A) AS iap format=22.15
    FROM T
    GROUP BY 1
    ORDER BY a ;
    QUIT;


    ACCOUNT_NUMBER        B         C                D    PRVN_A                 iap
    --------------------------------------------------------------------------------
    00000000481710428888  07Mar201  IP        175455.8  175455.8   0.000000000007276   ** Why not 0?
    00000000481710428888  09Nov201  WB        -63835.6  -63835.6   0.000000000007276
    00000000481710428888  23Nov201  WO         27074.9  -27074.9   0.000000000007276
    00000000481710428888  23Nov201  WO        49240.65  -49240.7   0.000000000007276
    00000000481710428888  23Nov201  WO        70265.56  -70265.6   0.000000000007276
    00000000481710428888  24Nov201  NP           34961     34961   0.000000000007276
    00000000481910257067  01Apr201  NP           47129     47129   0.000000000000000
    00000000481910257067  11Apr201  WO         3287.69  -3287.69   0.000000000000000
    00000000481910257067  22Mar201  IP         3287.69   3287.69   0.000000000000000
    00000000481910257067  27May201  WO           47129    -47129   0.000000000000000

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|
                                      ;
    ;

    * REDUCED ERROR BECASE SUM IS EXACT

    data t;
    input a b $ c $ d ;
    d=round(100*d);
    datalines;
    481710428888 24Nov2010 NP 34961.0000
    481710428888 07Mar2013 IP 175455.7500
    481710428888 09Nov2015 WB -63835.6400
    481710428888 23Nov2015 WO 27074.9000
    481710428888 23Nov2015 WO 49240.6500
    481710428888 23Nov2015 WO 70265.5600
    481910257067 01Apr2010 NP 47129.0000
    481910257067 27May2010 WO 47129.0000
    481910257067 22Mar2013 IP 3287.6900
    481910257067 11Apr2013 WO 3287.6900
    ;
    run;
    *             _                    _
     _ __ ___  __| |_   _  ___ ___  __| |   ___ _ __ _ __ ___  _ __
    | '__/ _ \/ _` | | | |/ __/ _ \/ _` |  / _ \ '__| '__/ _ \| '__|
    | | |  __/ (_| | |_| | (_|  __/ (_| | |  __/ |  | | | (_) | |
    |_|  \___|\__,_|\__,_|\___\___|\__,_|  \___|_|  |_|  \___/|_|

    ;

    * CLOSE TO INFINITE?;

    PROC SQL;
    SELECT DISTINCT
           put(a, z20.) AS ACCOUNT_NUMBER,
           b,
           c,
           d,
           (CASE WHEN c  = 'WO' THEN -1 ELSE 1 END) * d AS PRVN_A
           ,SUM (CALCULATED PRVN_A)/100 AS iap format=22.15
    FROM T
    GROUP BY 1
    ORDER BY a ;
    QUIT;

    ACCOUNT_NUMBER        B         C                D    PRVN_A                 iap
    ---------------------------------------------------------------------------------
    00000000481710428888  07Mar201  IP        17545575  17545575    0.000000000000000
    00000000481710428888  09Nov201  WB        -6383564  -6383564    0.000000000000000
    00000000481710428888  23Nov201  WO         2707490  -2707490    0.000000000000000
    00000000481710428888  23Nov201  WO         4924065  -4924065    0.000000000000000
    00000000481710428888  23Nov201  WO         7026556  -7026556    0.000000000000000
    00000000481710428888  24Nov201  NP         3496100   3496100    0.000000000000000
    00000000481910257067  01Apr201  NP         4712900   4712900    0.000000000000000
    00000000481910257067  11Apr201  WO          328769   -328769    0.000000000000000
    00000000481910257067  22Mar201  IP          328769    328769    0.000000000000000
    00000000481910257067  27May201  WO         4712900  -4712900    0.000000000000000

    *_        __ _       _ _                                _
    (_)_ __  / _(_)_ __ (_) |_ ___   _ __   ___ _ __  _ __ (_) ___  ___
    | | '_ \| |_| | '_ \| | __/ _ \ | '_ \ / _ \ '_ \| '_ \| |/ _ \/ __|
    | | | | |  _| | | | | | ||  __/ | |_) |  __/ | | | | | | |  __/\__ \
    |_|_| |_|_| |_|_| |_|_|\__\___| | .__/ \___|_| |_|_| |_|_|\___||___/
                                    |_|
    ;

    *INFINITE PRECISION;


    data t;
    input a b $ c $ d ;
    d=round(100*d);
    datalines;
    481710428888 24Nov2010 NP 34961.0000
    481710428888 07Mar2013 IP 175455.7500
    481710428888 09Nov2015 WB -63835.6400
    481710428888 23Nov2015 WO 27074.9000
    481710428888 23Nov2015 WO 49240.6500
    481710428888 23Nov2015 WO 70265.5600
    481910257067 01Apr2010 NP 47129.0000
    481910257067 27May2010 WO 47129.0000
    481910257067 22Mar2013 IP 3287.6900
    481910257067 11Apr2013 WO 3287.6900
    ;
    run;


    PROC SQL;
    SELECT DISTINCT
           put(a, z20.) AS ACCOUNT_NUMBER,
           b,
           c,
           d,
           (CASE WHEN c  = 'WO' THEN -1 ELSE 1 END) * d AS PRVN_A
           ,SUM (CALCULATED PRVN_A) AS iap format=22.15
    FROM T
    GROUP BY 1
    ORDER BY a ;
    QUIT;

    * INTEGERS no errors even if infinite number of decimals;

    ACCOUNT_NUMBER        B         C                D    PRVN_A                     iap
    ------------------------------------------------------------------------------------
    00000000481710428888  07Mar201  IP        17545575  17545575       0.000000000000000
    00000000481710428888  09Nov201  WB        -6383564  -6383564       0.000000000000000
    00000000481710428888  23Nov201  WO         2707490  -2707490       0.000000000000000
    00000000481710428888  23Nov201  WO         4924065  -4924065       0.000000000000000
    00000000481710428888  23Nov201  WO         7026556  -7026556       0.000000000000000
    00000000481710428888  24Nov201  NP         3496100   3496100       0.000000000000000
    00000000481910257067  01Apr201  NP         4712900   4712900       0.000000000000000
    00000000481910257067  11Apr201  WO          328769   -328769       0.000000000000000
    00000000481910257067  22Mar201  IP          328769    328769       0.000000000000000
    00000000481910257067  27May201  WO         4712900  -4712900       0.000000000000000

    *_        __ _       _ _               _      _
    (_)_ __  / _(_)_ __ (_) |_ ___   _ __ (_) ___| |_ _   _ _ __ ___
    | | '_ \| |_| | '_ \| | __/ _ \ | '_ \| |/ __| __| | | | '__/ _ \
    | | | | |  _| | | | | | ||  __/ | |_) | | (__| |_| |_| | | |  __/
    |_|_| |_|_| |_|_| |_|_|\__\___| | .__/|_|\___|\__|\__,_|_|  \___|
                                    |_|
    ;

    *INFINITE PRECISION IN PICTURED DOLLARS;

    proc format ;
       picture fix (round)
          other ="9.99999999999999999" (prefix='0.' mult=0.01);
    run;quit;


    data t;
    input a b $ c $ d ;
    d=round(100*d);
    datalines;
    481710428888 24Nov2010 NP 34961.0000
    481710428888 07Mar2013 IP 175455.7500
    481710428888 09Nov2015 WB -63835.6400
    481710428888 23Nov2015 WO 27074.9000
    481710428888 23Nov2015 WO 49240.6500
    481710428888 23Nov2015 WO 70265.5600
    481910257067 01Apr2010 NP 47129.0000
    481910257067 27May2010 WO 47129.0000
    481910257067 22Mar2013 IP 3287.6900
    481910257067 11Apr2013 WO 3287.6900
    ;
    run;


    PROC SQL;
    SELECT DISTINCT
           put(a, z20.) AS ACCOUNT_NUMBER,
           b,
           c,
           d,
           (CASE WHEN c  = 'WO' THEN -1 ELSE 1 END) * d AS PRVN_A
           ,SUM (CALCULATED PRVN_A) AS iap format=fix.
    FROM T
    GROUP BY 1
    ORDER BY a ;
    QUIT;



    * INTEGERS no errors even if infinite number of decimals;

    ACCOUNT_NUMBER        B         C                D    PRVN_A                     iap
    ------------------------------------------------------------------------------------
    00000000481710428888  07Mar201  IP        17545575  17545575       0.000000000000000
    00000000481710428888  09Nov201  WB        -6383564  -6383564       0.000000000000000
    00000000481710428888  23Nov201  WO         2707490  -2707490       0.000000000000000
    00000000481710428888  23Nov201  WO         4924065  -4924065       0.000000000000000
    00000000481710428888  23Nov201  WO         7026556  -7026556       0.000000000000000
    00000000481710428888  24Nov201  NP         3496100   3496100       0.000000000000000
    00000000481910257067  01Apr201  NP         4712900   4712900       0.000000000000000
    00000000481910257067  11Apr201  WO          328769   -328769       0.000000000000000
    00000000481910257067  22Mar201  IP          328769    328769       0.000000000000000
    00000000481910257067  27May201  WO         4712900  -4712900       0.000000000000000


