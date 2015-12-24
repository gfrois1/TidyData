---
title: "CodeBook of Get and Clean Data Project"
author: "gfrois"
date: "24 December 2015"
output: html_document
---
CodeBook of Get and Clean Data Project 

Source: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

Full Description at the site where the data was obtained:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Process

The script run_analysis.R performs the following process to clean up the data and create tiny data sets:

    Merge the training and test sets to create one data set.
    Reads features.txt and uses only the measurements on the mean and standard deviation for each measurement.
    Reads activity_labels.txt and applies human readable activity names to name the activities in the data set.
    Labels the data set with descriptive names. 
    Merges the features with activity labels and subject IDs. 

Variables

TrainSubject  contains "UCI HAR Dataset/train/Subject_train.txt"
TrainActivity contains "UCI HAR Dataset/train/y_train.txt"
TrainFeature  contains "UCI HAR Dataset/train/X_train.txt"

TestSubject  contains "UCI HAR Dataset/test/Subject_test.txt"
TestActivity contains "UCI HAR Dataset/test/y_test.txt"
TestFeature  contains "UCI HAR Dataset/test/X_test.txt",

Subject  contains TrainSubject merged with TestSubject
Activity contains TrainActivity merged with TestActivity
Feature  contains TrainFeature merged with TestFeature
FeatureNames       contains "UCI HAR Dataset/features.txt from Supporting Metadata
colnames(Feature)  naming the columns

colnames(Subject)  = "Subject"
colnames(Activity) = "Activity"

MergedData         contains Feature,Activity,Subject merged together

MeanStdCols    Extract the column indices that have either mean or std in them.

requiredColumns    Add Activity and Subject columns to the list
dim(MergedData)    dimension of MergedData

ExtractedData   
dim(ExtractedData)

change Activity field type in ExtractedData from numeric to character to accept Activity names from metadata ActivityLabels:
ActivityLabels contains Supporting Metadata
ExtractedData$Activity 

ExtractedData$Activity    factor the Activity variable in

Labels the data set with descriptive variable names
names(ExtractedData)=gsub("Acc", "Accelerometer", names(ExtractedData))  ## names variables from and to
names(ExtractedData)


ExtractedData$Subject    set Subject as a factor variable.
ExtractedData       

TidyData    create TidyData as a data set with average for each Activity and Subject

TidyData = TidyData[order..   order the entries in TidyData

write data file "TidyDataSet.txt"
write.table(TidyData, file = "TidyDataSet.txt", row.names = FALSE)

6 first rows:
> head(TidyData)
    Subject           Activity TimeBodyAccelerometerMean()-X
1         1             LAYING                     0.2215982
31        1            SITTING                     0.2612376
61        1           STANDING                     0.2789176
91        1            WALKING                     0.2773308
121       1 WALKING_DOWNSTAIRS                     0.2891883
151       1   WALKING_UPSTAIRS                     0.2554617
    TimeBodyAccelerometerMean()-Y TimeBodyAccelerometerMean()-Z
1                    -0.040513953                    -0.1132036
31                   -0.001308288                    -0.1045442
61                   -0.016137590                    -0.1106018
91                   -0.017383819                    -0.1111481
121                  -0.009918505                    -0.1075662
151                  -0.023953149                    -0.0973020
    TimeBodyAccelerometerSTD()-X TimeBodyAccelerometerSTD()-Y
1                    -0.92805647                 -0.836827406
31                   -0.97722901                 -0.922618642
61                   -0.99575990                 -0.973190056
91                   -0.28374026                  0.114461337
121                   0.03003534                 -0.031935943
151                  -0.35470803                 -0.002320265
    TimeBodyAccelerometerSTD()-Z TimeGravityAccelerometerMean()-X
1                    -0.82606140                       -0.2488818
31                   -0.93958629                        0.8315099
61                   -0.97977588                        0.9429520
91                   -0.26002790                        0.9352232
121                  -0.23043421                        0.9318744
151                  -0.01947924                        0.8933511
    TimeGravityAccelerometerMean()-Y TimeGravityAccelerometerMean()-Z
1                          0.7055498                       0.44581772
31                         0.2044116                       0.33204370
61                        -0.2729838                       0.01349058
91                        -0.2821650                      -0.06810286
121                       -0.2666103                      -0.06211996
151                       -0.3621534                      -0.07540294
    TimeGravityAccelerometerSTD()-X TimeGravityAccelerometerSTD()-Y
1                        -0.8968300                      -0.9077200
31                       -0.9684571                      -0.9355171
61                       -0.9937630                      -0.9812260
91                       -0.9766096                      -0.9713060
121                      -0.9505598                      -0.9370187
151                      -0.9563670                      -0.9528492
    TimeGravityAccelerometerSTD()-Z TimeBodyAccelerometerJerkMean()-X
1                        -0.8523663                        0.08108653
31                       -0.9490409                        0.07748252
61                       -0.9763241                        0.07537665
91                       -0.9477172                        0.07404163
121                      -0.8959397                        0.05415532
151                      -0.9123794                        0.10137273
    TimeBodyAccelerometerJerkMean()-Y TimeBodyAccelerometerJerkMean()-Z
1                        0.0038382040                       0.010834236
31                      -0.0006191028                      -0.003367792
61                       0.0079757309                      -0.003685250
91                       0.0282721096                      -0.004168406
121                      0.0296504490                      -0.010971973
151                      0.0194863076                      -0.045562545
    TimeBodyAccelerometerJerkSTD()-X TimeBodyAccelerometerJerkSTD()-Y
1                        -0.95848211                       -0.9241493
31                       -0.98643071                       -0.9813720
61                       -0.99460454                       -0.9856487
91                       -0.11361560                        0.0670025
121                      -0.01228386                       -0.1016014
151                      -0.44684389                       -0.3782744
    TimeBodyAccelerometerJerkSTD()-Z TimeBodyGyroscopeMean()-X
1                         -0.9548551               -0.01655309
31                        -0.9879108               -0.04535006
61                        -0.9922512               -0.02398773
91                        -0.5026998               -0.04183096
121                       -0.3457350               -0.03507819
151                       -0.7065935                0.05054938
    TimeBodyGyroscopeMean()-Y TimeBodyGyroscopeMean()-Z
1                 -0.06448612                0.14868944
31                -0.09192415                0.06293138
61                -0.05939722                0.07480075
91                -0.06953005                0.08494482
121               -0.09093713                0.09008501
151               -0.16617002                0.05835955
    TimeBodyGyroscopeSTD()-X TimeBodyGyroscopeSTD()-Y
1                 -0.8735439             -0.951090440
31                -0.9772113             -0.966473895
61                -0.9871919             -0.987734440
91                -0.4735355             -0.054607769
121               -0.4580305             -0.126349195
151               -0.5448711              0.004105184
    TimeBodyGyroscopeSTD()-Z TimeBodyGyroscopeJerkMean()-X
1                 -0.9082847                   -0.10727095
31                -0.9414259                   -0.09367938
61                -0.9806456                   -0.09960921
91                -0.3442666                   -0.08999754
121               -0.1247025                   -0.07395920
151               -0.5071687                   -0.12223277
    TimeBodyGyroscopeJerkMean()-Y TimeBodyGyroscopeJerkMean()-Z
1                     -0.04151729                   -0.07405012
31                    -0.04021181                   -0.04670263
61                    -0.04406279                   -0.04895055
91                    -0.03984287                   -0.04613093
121                   -0.04399028                   -0.02704611
151                   -0.04214859                   -0.04071255
    TimeBodyGyroscopeJerkSTD()-X TimeBodyGyroscopeJerkSTD()-Y
1                     -0.9186085                   -0.9679072
31                    -0.9917316                   -0.9895181
61                    -0.9929451                   -0.9951379
91                    -0.2074219                   -0.3044685
121                   -0.4870273                   -0.2388248
151                   -0.6147865                   -0.6016967
    TimeBodyGyroscopeJerkSTD()-Z TimeBodyAccelerometerMagnitudeMean()
1                     -0.9577902                          -0.84192915
31                    -0.9879358                          -0.94853679
61                    -0.9921085                          -0.98427821
91                    -0.4042555                          -0.13697118
121                   -0.2687615                           0.02718829
151                   -0.6063320                          -0.12992763
    TimeBodyAccelerometerMagnitudeSTD()
1                           -0.79514486
31                          -0.92707842
61                          -0.98194293
91                          -0.21968865
121                          0.01988435
151                         -0.32497093
    TimeGravityAccelerometerMagnitudeMean()
1                               -0.84192915
31                              -0.94853679
61                              -0.98427821
91                              -0.13697118
121                              0.02718829
151                             -0.12992763
    TimeGravityAccelerometerMagnitudeSTD()
1                              -0.79514486
31                             -0.92707842
61                             -0.98194293
91                             -0.21968865
121                             0.01988435
151                            -0.32497093
    TimeBodyAccelerometerJerkMagnitudeMean()
1                                -0.95439626
31                               -0.98736420
61                               -0.99236779
91                               -0.14142881
121                              -0.08944748
151                              -0.46650345
    TimeBodyAccelerometerJerkMagnitudeSTD()
1                               -0.92824563
31                              -0.98412002
61                              -0.99309621
91                              -0.07447175
121                             -0.02578772
151                             -0.47899162
    TimeBodyGyroscopeMagnitudeMean() TimeBodyGyroscopeMagnitudeSTD()
1                        -0.87475955                      -0.8190102
31                       -0.93089249                      -0.9345318
61                       -0.97649379                      -0.9786900
91                       -0.16097955                      -0.1869784
121                      -0.07574125                      -0.2257244
151                      -0.12673559                      -0.1486193
    TimeBodyGyroscopeJerkMagnitudeMean()
1                             -0.9634610
31                            -0.9919763
61                            -0.9949668
91                            -0.2987037
121                           -0.2954638
151                           -0.5948829
    TimeBodyGyroscopeJerkMagnitudeSTD()
1                            -0.9358410
31                           -0.9883087
61                           -0.9947332
91                           -0.3253249
121                          -0.3065106
151                          -0.6485530
    FrequencyBodyAccelerometerMean()-X
1                          -0.93909905
31                         -0.97964124
61                         -0.99524993
91                         -0.20279431
121                         0.03822918
151                        -0.40432178
    FrequencyBodyAccelerometerMean()-Y
1                         -0.867065205
31                        -0.944084550
61                        -0.977070848
91                         0.089712726
121                        0.001549908
151                       -0.190976721
    FrequencyBodyAccelerometerMean()-Z
1                           -0.8826669
31                          -0.9591849
61                          -0.9852971
91                          -0.3315601
121                         -0.2255745
151                         -0.4333497
    FrequencyBodyAccelerometerSTD()-X FrequencyBodyAccelerometerSTD()-Y
1                         -0.92443743                       -0.83362556
31                        -0.97641231                       -0.91727501
61                        -0.99602835                       -0.97229310
91                        -0.31913472                        0.05604001
121                        0.02433084                       -0.11296374
151                       -0.33742819                        0.02176951
    FrequencyBodyAccelerometerSTD()-Z
1                         -0.81289156
31                        -0.93446956
61                        -0.97793726
91                        -0.27968675
121                       -0.29792789
151                        0.08595655
    FrequencyBodyAccelerometerMeanFreq()-X
1                              -0.15879267
31                             -0.04951360
61                              0.08651536
91                             -0.20754837
121                            -0.30739520
151                            -0.41873500
    FrequencyBodyAccelerometerMeanFreq()-Y
1                               0.09753484
31                              0.07594608
61                              0.11747895
91                              0.11309365
121                             0.06322008
151                            -0.16069721
    FrequencyBodyAccelerometerMeanFreq()-Z
1                               0.08943766
31                              0.23882987
61                              0.24485859
91                              0.04972652
121                             0.29432270
151                            -0.52011479
    FrequencyBodyAccelerometerJerkMean()-X
1                              -0.95707388
31                             -0.98659702
61                             -0.99463080
91                             -0.17054696
121                            -0.02766387
151                            -0.47987525
    FrequencyBodyAccelerometerJerkMean()-Y
1                              -0.92246261
31                             -0.98157947
61                             -0.98541870
91                             -0.03522552
121                            -0.12866716
151                            -0.41344459
    FrequencyBodyAccelerometerJerkMean()-Z
1                               -0.9480609
31                              -0.9860531
61                              -0.9907522
91                              -0.4689992
121                             -0.2883347
151                             -0.6854744
    FrequencyBodyAccelerometerJerkSTD()-X
1                              -0.9641607
31                             -0.9874930
61                             -0.9950738
91                             -0.1335866
121                            -0.0863279
151                            -0.4619070
    FrequencyBodyAccelerometerJerkSTD()-Y
1                              -0.9322179
31                             -0.9825139
61                             -0.9870182
91                              0.1067399
121                            -0.1345800
151                            -0.3817771
    FrequencyBodyAccelerometerJerkSTD()-Z
1                              -0.9605870
31                             -0.9883392
61                             -0.9923498
91                             -0.5347134
121                            -0.4017215
151                            -0.7260402
    FrequencyBodyAccelerometerJerkMeanFreq()-X
1                                    0.1324191
31                                   0.2566108
61                                   0.3141829
91                                  -0.2092620
121                                 -0.2531643
151                                 -0.3770231
    FrequencyBodyAccelerometerJerkMeanFreq()-Y
1                                   0.02451362
31                                  0.04754378
61                                  0.03916190
91                                 -0.38623714
121                                -0.33758970
151                                -0.50949553
    FrequencyBodyAccelerometerJerkMeanFreq()-Z
1                                  0.024387945
31                                 0.092392003
61                                 0.138581479
91                                -0.185530281
121                                0.009372239
151                               -0.551104284
    FrequencyBodyGyroscopeMean()-X FrequencyBodyGyroscopeMean()-Y
1                       -0.8502492                    -0.95219149
31                      -0.9761615                    -0.97583859
61                      -0.9863868                    -0.98898446
91                      -0.3390322                    -0.10305942
121                     -0.3524496                    -0.05570225
151                     -0.4926117                    -0.31947461
    FrequencyBodyGyroscopeMean()-Z FrequencyBodyGyroscopeSTD()-X
1                      -0.90930272                    -0.8822965
31                     -0.95131554                    -0.9779042
61                     -0.98077312                    -0.9874971
91                     -0.25594094                    -0.5166919
121                    -0.03186943                    -0.4954225
151                    -0.45359721                    -0.5658925
    FrequencyBodyGyroscopeSTD()-Y FrequencyBodyGyroscopeSTD()-Z
1                     -0.95123205                    -0.9165825
31                    -0.96234504                    -0.9439178
61                    -0.98710773                    -0.9823453
91                    -0.03350816                    -0.4365622
121                   -0.18141473                    -0.2384436
151                    0.15153891                    -0.5717078
    FrequencyBodyGyroscopeMeanFreq()-X
1                         -0.003546796
31                         0.189153021
61                        -0.120293021
91                         0.014784499
121                       -0.100453729
151                       -0.187450248
    FrequencyBodyGyroscopeMeanFreq()-Y
1                          -0.09152913
31                          0.06312707
61                         -0.04471920
91                         -0.06577462
121                         0.08255115
151                        -0.47357479
    FrequencyBodyGyroscopeMeanFreq()-Z
1                         0.0104581257
31                       -0.0297839207
61                        0.1006076351
91                        0.0007733216
121                      -0.0756762068
151                      -0.1333739043
    FrequencyBodyAccelerometerMagnitudeMean()
1                                 -0.86176765
31                                -0.94778292
61                                -0.98535636
91                                -0.12862345
121                                0.09658453
151                               -0.35239594
    FrequencyBodyAccelerometerMagnitudeSTD()
1                                 -0.7983009
31                                -0.9284448
61                                -0.9823138
91                                -0.3980326
121                               -0.1865303
151                               -0.4162601
    FrequencyBodyAccelerometerMagnitudeMeanFreq()
1                                      0.08640856
31                                     0.23665501
61                                     0.28455529
91                                     0.19064372
121                                    0.11918714
151                                   -0.09774335
    FrequencyBodyAccelerometerJerkMagnitudeMean()
1                                     -0.93330036
31                                    -0.98526213
61                                    -0.99254248
91                                    -0.05711940
121                                    0.02621849
151                                   -0.44265216
    FrequencyBodyAccelerometerJerkMagnitudeSTD()
1                                     -0.9218040
31                                    -0.9816062
61                                    -0.9925360
91                                    -0.1034924
121                                   -0.1040523
151                                   -0.5330599
    FrequencyBodyAccelerometerJerkMagnitudeMeanFreq()
1                                          0.26639115
31                                         0.35185220
61                                         0.42222010
91                                         0.09382218
121                                        0.07649155
151                                        0.08535241
    FrequencyBodyGyroscopeMagnitudeMean()
1                              -0.8621902
31                             -0.9584356
61                             -0.9846176
91                             -0.1992526
121                            -0.1857203
151                            -0.3259615
    FrequencyBodyGyroscopeMagnitudeSTD()
1                             -0.8243194
31                            -0.9321984
61                            -0.9784661
91                            -0.3210180
121                           -0.3983504
151                           -0.1829855
    FrequencyBodyGyroscopeMagnitudeMeanFreq()
1                               -0.1397750127
31                              -0.0002621867
61                              -0.0286057725
91                               0.2688443675
121                              0.3496138955
151                             -0.2193033761
    FrequencyBodyGyroscopeJerkMagnitudeMean()
1                                  -0.9423669
31                                 -0.9897975
61                                 -0.9948154
91                                 -0.3193086
121                                -0.2819634
151                                -0.6346651
    FrequencyBodyGyroscopeJerkMagnitudeSTD()
1                                 -0.9326607
31                                -0.9870496
61                                -0.9946711
91                                -0.3816019
121                               -0.3919199
151                               -0.6939305
    FrequencyBodyGyroscopeJerkMagnitudeMeanFreq()
1                                       0.1764859
31                                      0.1847759
61                                      0.3344987
91                                      0.1906634
121                                     0.1900007
151                                     0.1142773
    angle(TimeBodyAccelerometerMean,gravity)
1                               0.0213659656
31                              0.0274415479
61                             -0.0002223407
91                              0.0604537474
121                            -0.0026951252
151                             0.0960860762
    angle(TimeBodyAccelerometerJerkMean),gravityMean)
1                                         0.003060407
31                                        0.029709788
61                                        0.021963783
91                                       -0.007930378
121                                       0.089931687
151                                      -0.061083841
    angle(TimeBodyGyroscopeMean,gravityMean)
1                               -0.001666985
31                               0.067698134
61                              -0.033793838
91                               0.013059491
121                              0.063338285
151                             -0.194699963
    angle(TimeBodyGyroscopeJerkMean,gravityMean) angle(X,gravityMean)
1                                     0.08443716            0.4267062
31                                   -0.06488162           -0.5912475
61                                   -0.02792293           -0.7434079
91                                   -0.01874319           -0.7292472
121                                  -0.03997685           -0.7444838
151                                   0.06568357           -0.6471957
    angle(Y,gravityMean) angle(Z,gravityMean)
1            -0.52034382          -0.35241311
31           -0.06046603          -0.21801723
61            0.27017503           0.01225285
91            0.27695302           0.06885891
121           0.26724578           0.06500471
151           0.33476328           0.07416637


