---
layout: post
category: Python
title: statsmodels memo
tagline: by SunHaozhe
tags: 
  - Python
  - API
  - Machine learning
mathjax: true
comments: true
published: true
---

Import statsmodels:

```python
import statsmodels.api as sm
```

# Ordinary Least Squares

Fit OLS:

```python
regression_results = sm.OLS(y_train, X_train.assign(const=1)).fit()
# regression_results is a statsmodels.regression.linear_model.RegressionResultsWrapper
```

Summarize the regression results:

```python
print(regression_results.summary())
```

```
                            OLS Regression Results                            
==============================================================================
Dep. Variable:              SalePrice   R-squared:                       0.921
Model:                            OLS   Adj. R-squared:                  0.909
Method:                 Least Squares   F-statistic:                     79.79
Date:                Tue, 31 Dec 2019   Prob (F-statistic):               0.00
Time:                        12:18:02   Log-Likelihood:                -16695.
No. Observations:                1460   AIC:                         3.376e+04
Df Residuals:                    1274   BIC:                         3.475e+04
Df Model:                         185                                         
Covariance Type:            nonrobust                                         
=========================================================================================
                            coef    std err          t      P>|t|      [0.025      0.975]
-----------------------------------------------------------------------------------------
MSSubClass               -9.7062     85.213     -0.114      0.909    -176.880     157.467
LotArea                   0.7020      0.108      6.511      0.000       0.490       0.914
OverallQual            7995.0504   1016.388      7.866      0.000    6001.071    9989.030
OverallCond            5377.8889    868.955      6.189      0.000    3673.149    7082.629
YearBuilt               325.5002     73.420      4.433      0.000     181.464     469.537
YearRemodAdd            104.8320     55.198      1.899      0.058      -3.457     213.121
BsmtFinSF1               17.9310      2.069      8.667      0.000      13.872      21.990
BsmtFinSF2                5.3753      3.450      1.558      0.119      -1.393      12.144
BsmtUnfSF                -4.1837      1.987     -2.105      0.035      -8.082      -0.285
TotalBsmtSF              19.1226      3.137      6.096      0.000      12.969      25.276
1stFlrSF                 17.7089      6.015      2.944      0.003       5.908      29.510
2ndFlrSF                 32.6119      5.371      6.072      0.000      22.075      43.149
LowQualFinSF            -12.8942     13.653     -0.944      0.345     -39.680      13.891
GrLivArea                37.4266      5.459      6.855      0.000      26.716      48.137
BsmtFullBath           1544.3255   1963.516      0.787      0.432   -2307.754    5396.406
BsmtHalfBath            370.4441   3108.148      0.119      0.905   -5727.206    6468.094
FullBath               2525.0854   2236.017      1.129      0.259   -1861.596    6911.767
HalfBath               -149.2172   2131.489     -0.070      0.944   -4330.831    4032.396
BedroomAbvGr          -5492.6127   1377.551     -3.987      0.000   -8195.131   -2790.094
KitchenAbvGr          -1.589e+04   5716.765     -2.780      0.006   -2.71e+04   -4677.082
TotRmsAbvGrd           1366.0063    972.579      1.405      0.160    -542.026    3274.038
Fireplaces             2758.2809   1368.941      2.015      0.044      72.655    5443.907
GarageCars             4296.1362   2215.722      1.939      0.053     -50.730    8643.002
GarageArea               13.1261      7.612      1.724      0.085      -1.807      28.059
WoodDeckSF               13.6075      5.943      2.290      0.022       1.948      25.267
OpenPorchSF              12.2324     11.797      1.037      0.300     -10.911      35.376
EnclosedPorch             5.3769     12.768      0.421      0.674     -19.671      30.425
3SsnPorch                24.0018     23.079      1.040      0.299     -21.275      69.278
ScreenPorch              37.0246     12.567      2.946      0.003      12.371      61.678
PoolArea                 71.3912     18.279      3.906      0.000      35.532     107.251
MiscVal                  -0.3282      1.466     -0.224      0.823      -3.203       2.547
MoSold                 -629.3505    252.934     -2.488      0.013   -1125.563    -133.138
YrSold                 -179.7022    523.388     -0.343      0.731   -1206.499     847.095
MSZoning_FV             3.09e+04   1.22e+04      2.537      0.011    7004.086    5.48e+04
MSZoning_RH            2.403e+04   1.23e+04      1.961      0.050     -13.023    4.81e+04
MSZoning_RL            2.591e+04   1.04e+04      2.482      0.013    5430.959    4.64e+04
MSZoning_RM            2.498e+04   9767.635      2.558      0.011    5820.056    4.41e+04
Street_Pave            3.886e+04   1.23e+04      3.172      0.002    1.48e+04    6.29e+04
LotShape_IR2           4487.5720   4310.410      1.041      0.298   -3968.711    1.29e+04
LotShape_IR3           3606.4781   8782.142      0.411      0.681   -1.36e+04    2.08e+04
LotShape_Reg            581.4459   1659.526      0.350      0.726   -2674.259    3837.150
LandContour_HLS        1.377e+04   5274.095      2.611      0.009    3422.893    2.41e+04
LandContour_Low       -4101.8814   6505.104     -0.631      0.528   -1.69e+04    8660.013
LandContour_Lvl        7264.2900   3799.244      1.912      0.056    -189.172    1.47e+04
Utilities_NoSeWa      -2.945e+04   2.64e+04     -1.117      0.264   -8.12e+04    2.23e+04
LotConfig_CulDSac      7683.5534   3317.330      2.316      0.021    1175.523    1.42e+04
LotConfig_FR2         -5782.6223   4146.108     -1.395      0.163   -1.39e+04    2351.328
LotConfig_FR3         -1.338e+04    1.3e+04     -1.026      0.305    -3.9e+04    1.22e+04
LotConfig_Inside      -1223.4932   1799.654     -0.680      0.497   -4754.104    2307.118
LandSlope_Mod          1.054e+04   4024.800      2.618      0.009    2639.342    1.84e+04
LandSlope_Sev         -2.553e+04   1.11e+04     -2.308      0.021   -4.72e+04   -3826.900
Neighborhood_Blueste  -2590.8335   1.93e+04     -0.134      0.893   -4.05e+04    3.53e+04
Neighborhood_BrDale    8307.2146   1.11e+04      0.748      0.455   -1.35e+04    3.01e+04
Neighborhood_BrkSide  -1847.5215   9474.078     -0.195      0.845   -2.04e+04    1.67e+04
Neighborhood_ClearCr  -1.285e+04   9402.186     -1.366      0.172   -3.13e+04    5599.982
Neighborhood_CollgCr  -9675.1018   7320.280     -1.322      0.187    -2.4e+04    4686.027
Neighborhood_Crawfor   9576.1151   8653.032      1.107      0.269   -7399.643    2.66e+04
Neighborhood_Edwards  -1.675e+04   8062.599     -2.078      0.038   -3.26e+04    -933.809
Neighborhood_Gilbert  -1.372e+04   7830.740     -1.752      0.080   -2.91e+04    1640.935
Neighborhood_IDOTRR   -7378.2773   1.08e+04     -0.682      0.495   -2.86e+04    1.38e+04
Neighborhood_MeadowV  -1609.7582   1.14e+04     -0.141      0.888   -2.39e+04    2.07e+04
Neighborhood_Mitchel  -2.036e+04   8262.112     -2.464      0.014   -3.66e+04   -4152.843
Neighborhood_NAmes    -1.449e+04   7887.235     -1.837      0.066      -3e+04     983.669
Neighborhood_NPkVill   8214.5230   1.43e+04      0.574      0.566   -1.98e+04    3.63e+04
Neighborhood_NWAmes    -2.05e+04   8129.410     -2.522      0.012   -3.64e+04   -4550.979
Neighborhood_NoRidge   2.889e+04   8380.757      3.447      0.001    1.24e+04    4.53e+04
Neighborhood_NridgHt   2.457e+04   7363.439      3.337      0.001    1.01e+04     3.9e+04
Neighborhood_OldTown    -1.3e+04   9654.412     -1.346      0.178   -3.19e+04    5944.138
Neighborhood_SWISU    -9498.7723   9808.192     -0.968      0.333   -2.87e+04    9743.212
Neighborhood_Sawyer    -1.02e+04   8213.937     -1.241      0.215   -2.63e+04    5917.717
Neighborhood_SawyerW  -6160.8169   7839.757     -0.786      0.432   -2.15e+04    9219.437
Neighborhood_Somerst    170.1025   8955.990      0.019      0.985   -1.74e+04    1.77e+04
Neighborhood_StoneBr   3.894e+04   8369.414      4.652      0.000    2.25e+04    5.54e+04
Neighborhood_Timber   -5900.0628   8352.264     -0.706      0.480   -2.23e+04    1.05e+04
Neighborhood_Veenker   3056.6958   1.07e+04      0.285      0.775    -1.8e+04    2.41e+04
Condition1_Feedr       3035.3133   5087.778      0.597      0.551   -6946.032     1.3e+04
Condition1_Norm        1.221e+04   4194.252      2.912      0.004    3985.961    2.04e+04
Condition1_PosA        7473.0237   1.03e+04      0.727      0.467   -1.27e+04    2.76e+04
Condition1_PosN        8076.9858   7598.333      1.063      0.288   -6829.634     2.3e+04
Condition1_RRAe       -1.693e+04   9355.393     -1.810      0.071   -3.53e+04    1424.001
Condition1_RRAn        6490.0857   6998.125      0.927      0.354   -7239.030    2.02e+04
Condition1_RRNe       -7278.1229   1.83e+04     -0.397      0.692   -4.33e+04    2.87e+04
Condition1_RRNn        3894.4359   1.31e+04      0.298      0.766   -2.18e+04    2.96e+04
Condition2_Feedr      -9591.0629    2.3e+04     -0.417      0.677   -5.47e+04    3.55e+04
Condition2_Norm       -7506.3703   1.96e+04     -0.383      0.702   -4.59e+04    3.09e+04
Condition2_PosA        1.981e+04   3.79e+04      0.522      0.602   -5.46e+04    9.42e+04
Condition2_PosN       -2.303e+05   2.76e+04     -8.355      0.000   -2.84e+05   -1.76e+05
Condition2_RRAe        -1.29e+05   4.67e+04     -2.762      0.006   -2.21e+05   -3.74e+04
Condition2_RRAn       -1.203e+04   3.19e+04     -0.377      0.706   -7.46e+04    5.05e+04
Condition2_RRNn       -9030.3998   2.71e+04     -0.334      0.739   -6.21e+04     4.4e+04
BldgType_2fmCon       -6227.4194   1.28e+04     -0.485      0.628   -3.14e+04     1.9e+04
BldgType_Duplex       -1012.4022   7433.930     -0.136      0.892   -1.56e+04    1.36e+04
BldgType_Twnhs        -2.535e+04   1.01e+04     -2.503      0.012   -4.52e+04   -5477.984
BldgType_TwnhsE       -2.313e+04   9171.676     -2.522      0.012   -4.11e+04   -5134.970
HouseStyle_1.5Unf      1.091e+04   7882.021      1.384      0.167   -4552.198    2.64e+04
HouseStyle_1Story      8846.7366   4321.439      2.047      0.041     368.818    1.73e+04
HouseStyle_2.5Fin     -1.702e+04   1.23e+04     -1.387      0.166   -4.11e+04    7055.921
HouseStyle_2.5Unf     -1.154e+04   9362.237     -1.233      0.218   -2.99e+04    6826.997
HouseStyle_2Story     -6393.0048   3541.457     -1.805      0.071   -1.33e+04     554.724
HouseStyle_SFoyer      7779.7007   6177.832      1.259      0.208   -4340.143    1.99e+04
HouseStyle_SLvl        7395.4107   5446.509      1.358      0.175   -3289.702    1.81e+04
RoofStyle_Gable        1165.6349   1.87e+04      0.062      0.950   -3.55e+04    3.79e+04
RoofStyle_Gambrel      4013.9263   2.05e+04      0.196      0.845   -3.61e+04    4.42e+04
RoofStyle_Hip          2794.1655   1.88e+04      0.149      0.882    -3.4e+04    3.96e+04
RoofStyle_Mansard      1.701e+04   2.18e+04      0.780      0.435   -2.58e+04    5.98e+04
RoofStyle_Shed         8.806e+04   3.54e+04      2.485      0.013    1.85e+04    1.58e+05
RoofMatl_CompShg        6.49e+05   3.29e+04     19.726      0.000    5.84e+05    7.13e+05
RoofMatl_Membran       7.357e+05   4.76e+04     15.453      0.000    6.42e+05    8.29e+05
RoofMatl_Metal         6.956e+05    4.7e+04     14.793      0.000    6.03e+05    7.88e+05
RoofMatl_Roll          6.501e+05   4.15e+04     15.670      0.000    5.69e+05    7.31e+05
RoofMatl_Tar&Grv       6.542e+05   3.78e+04     17.297      0.000     5.8e+05    7.28e+05
RoofMatl_WdShake        6.29e+05   3.66e+04     17.178      0.000    5.57e+05    7.01e+05
RoofMatl_WdShngl       7.264e+05   3.41e+04     21.279      0.000    6.59e+05    7.93e+05
Exterior1st_AsphShn   -1.052e+04   3.38e+04     -0.311      0.756   -7.69e+04    5.59e+04
Exterior1st_BrkComm   -1.114e+04   2.83e+04     -0.394      0.694   -6.67e+04    4.44e+04
Exterior1st_BrkFace    6825.7077   1.25e+04      0.546      0.585   -1.77e+04    3.14e+04
Exterior1st_CBlock    -1.385e+04   1.38e+04     -1.007      0.314   -4.08e+04    1.31e+04
Exterior1st_CemntBd   -1.365e+04   1.92e+04     -0.712      0.476   -5.12e+04    2.39e+04
Exterior1st_HdBoard    -1.24e+04   1.26e+04     -0.986      0.324   -3.71e+04    1.23e+04
Exterior1st_ImStucc   -6.737e+04   2.84e+04     -2.372      0.018   -1.23e+05   -1.17e+04
Exterior1st_MetalSd   -1768.8055   1.45e+04     -0.122      0.903   -3.02e+04    2.66e+04
Exterior1st_Plywood   -1.651e+04   1.24e+04     -1.327      0.185   -4.09e+04    7903.662
Exterior1st_Stone     -1.357e+04   2.41e+04     -0.562      0.574   -6.09e+04    3.38e+04
Exterior1st_Stucco    -3662.3756   1.38e+04     -0.266      0.790   -3.07e+04    2.34e+04
Exterior1st_VinylSd   -1.633e+04   1.32e+04     -1.240      0.215   -4.22e+04    9505.295
Exterior1st_Wd Sdng   -1.239e+04    1.2e+04     -1.029      0.304    -3.6e+04    1.12e+04
Exterior1st_WdShing   -4980.9823    1.3e+04     -0.382      0.703   -3.06e+04    2.06e+04
Exterior2nd_AsphShn    6790.3360   2.26e+04      0.300      0.764   -3.76e+04    5.12e+04
Exterior2nd_Brk Cmn     1.39e+04   2.06e+04      0.675      0.500   -2.65e+04    5.43e+04
Exterior2nd_BrkFace   -1477.1404   1.32e+04     -0.112      0.911   -2.73e+04    2.44e+04
Exterior2nd_CBlock    -1.385e+04   1.38e+04     -1.007      0.314   -4.08e+04    1.31e+04
Exterior2nd_CmentBd    1.242e+04   1.91e+04      0.651      0.515    -2.5e+04    4.99e+04
Exterior2nd_HdBoard    7217.8047   1.23e+04      0.585      0.558    -1.7e+04    3.14e+04
Exterior2nd_ImStucc    3.276e+04   1.43e+04      2.290      0.022    4696.466    6.08e+04
Exterior2nd_MetalSd    2063.7813   1.43e+04      0.144      0.885    -2.6e+04    3.01e+04
Exterior2nd_Other     -6815.7656   2.81e+04     -0.242      0.809    -6.2e+04    4.84e+04
Exterior2nd_Plywood    8246.1108    1.2e+04      0.689      0.491   -1.52e+04    3.17e+04
Exterior2nd_Stone      -1.09e+04   1.72e+04     -0.634      0.526   -4.46e+04    2.28e+04
Exterior2nd_Stucco     1788.4981   1.36e+04      0.132      0.895   -2.48e+04    2.84e+04
Exterior2nd_VinylSd    1.576e+04   1.29e+04      1.222      0.222   -9544.003    4.11e+04
Exterior2nd_Wd Sdng    9923.3814   1.18e+04      0.839      0.402   -1.33e+04    3.31e+04
Exterior2nd_Wd Shng    2629.6628   1.24e+04      0.213      0.832   -2.16e+04    2.69e+04
ExterQual_Fa          -8528.5582   1.08e+04     -0.787      0.432   -2.98e+04    1.27e+04
ExterQual_Gd           -3.09e+04   4781.408     -6.462      0.000   -4.03e+04   -2.15e+04
ExterQual_TA          -3.084e+04   5349.931     -5.765      0.000   -4.13e+04   -2.03e+04
ExterCond_Fa          -2927.8023   1.88e+04     -0.156      0.876   -3.98e+04     3.4e+04
ExterCond_Gd          -8100.6504    1.8e+04     -0.451      0.652   -4.34e+04    2.72e+04
ExterCond_Po           1.141e+04   3.27e+04      0.349      0.727   -5.28e+04    7.56e+04
ExterCond_TA          -5395.6977   1.79e+04     -0.301      0.764   -4.06e+04    2.98e+04
Foundation_CBlock      1815.4754   3180.954      0.571      0.568   -4425.008    8055.959
Foundation_PConc       4843.8033   3497.060      1.385      0.166   -2016.826    1.17e+04
Foundation_Slab        8597.5525   7831.093      1.098      0.272   -6765.703     2.4e+04
Foundation_Stone       1122.2502   1.09e+04      0.103      0.918   -2.02e+04    2.24e+04
Foundation_Wood       -3.322e+04   1.51e+04     -2.202      0.028   -6.28e+04   -3623.567
Heating_GasA          -6917.4140   2.53e+04     -0.273      0.785   -5.66e+04    4.28e+04
Heating_GasW          -1.549e+04   2.62e+04     -0.592      0.554   -6.68e+04    3.58e+04
Heating_Grav          -1.447e+04   2.75e+04     -0.527      0.598   -6.83e+04    3.94e+04
Heating_OthW          -4.535e+04   3.17e+04     -1.433      0.152   -1.07e+05    1.67e+04
Heating_Wall           8977.4923   2.92e+04      0.307      0.759   -4.83e+04    6.63e+04
HeatingQC_Fa          -1474.5099   4795.773     -0.307      0.759   -1.09e+04    7933.970
HeatingQC_Gd          -3697.5228   2135.317     -1.732      0.084   -7886.648     491.602
HeatingQC_Po           7968.9287   2.74e+04      0.291      0.771   -4.58e+04    6.18e+04
HeatingQC_TA          -4346.9132   2115.519     -2.055      0.040   -8497.197    -196.630
CentralAir_Y          -3390.7932   3863.428     -0.878      0.380    -1.1e+04    4188.588
KitchenQual_Fa         -2.11e+04   6340.248     -3.329      0.001   -3.35e+04   -8665.178
KitchenQual_Gd         -2.78e+04   3480.001     -7.987      0.000   -3.46e+04    -2.1e+04
KitchenQual_TA        -2.536e+04   3984.072     -6.366      0.000   -3.32e+04   -1.75e+04
Functional_Maj2         230.1207   1.36e+04      0.017      0.986   -2.64e+04    2.69e+04
Functional_Min1        4184.2611   8613.483      0.486      0.627   -1.27e+04    2.11e+04
Functional_Min2        8541.8612   8554.828      0.998      0.318   -8241.238    2.53e+04
Functional_Mod        -7162.5851   1.05e+04     -0.679      0.497   -2.78e+04    1.35e+04
Functional_Sev        -6.026e+04   2.75e+04     -2.190      0.029   -1.14e+05   -6273.962
Functional_Typ         1.963e+04   7386.534      2.657      0.008    5135.535    3.41e+04
PavedDrive_P          -3247.1796   5557.619     -0.584      0.559   -1.42e+04    7655.912
PavedDrive_Y          -2035.7836   3435.093     -0.593      0.554   -8774.844    4703.277
SaleType_CWD           2.325e+04   1.33e+04      1.745      0.081   -2893.062    4.94e+04
SaleType_Con           3.533e+04   1.83e+04      1.926      0.054    -664.162    7.13e+04
SaleType_ConLD         1.682e+04   9992.758      1.683      0.093   -2787.399    3.64e+04
SaleType_ConLI         9656.7861   1.19e+04      0.813      0.417   -1.37e+04     3.3e+04
SaleType_ConLw        -2272.8110   1.24e+04     -0.184      0.854   -2.66e+04     2.2e+04
SaleType_New           3.472e+04    1.6e+04      2.169      0.030    3310.780    6.61e+04
SaleType_Oth           1.864e+04    1.5e+04      1.244      0.214   -1.08e+04     4.8e+04
SaleType_WD             541.9897   4328.000      0.125      0.900   -7948.801    9032.780
SaleCondition_AdjLand  8244.9837   1.45e+04      0.570      0.569   -2.01e+04    3.66e+04
SaleCondition_Alloca   4978.4162   8750.684      0.569      0.570   -1.22e+04    2.21e+04
SaleCondition_Family  -1417.1134   6306.408     -0.225      0.822   -1.38e+04     1.1e+04
SaleCondition_Normal   6526.6321   2969.845      2.198      0.028     700.308    1.24e+04
SaleCondition_Partial -9505.3208   1.54e+04     -0.616      0.538   -3.98e+04    2.08e+04
const                 -1.177e+06   1.06e+06     -1.108      0.268   -3.26e+06    9.06e+05
==============================================================================
Omnibus:                      498.410   Durbin-Watson:                   1.919
Prob(Omnibus):                  0.000   Jarque-Bera (JB):            12402.837
Skew:                           1.017   Prob(JB):                         0.00
Kurtosis:                      17.133   Cond. No.                     1.24e+16
==============================================================================

Warnings:
[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
[2] The smallest eigenvalue is 2.09e-21. This might indicate that there are
strong multicollinearity problems or that the design matrix is singular.
```





