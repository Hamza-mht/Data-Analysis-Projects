```python
# Import Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns 
```


```python
# Loading dataset
df = pd.read_excel('C:/Users/Mahtaoui/Desktop/Projets Data/USA Shopping trends/USA_Shopping_Trends.xlsx')
```


```python
df.head()             # preview first rows
df.info()             # check types & nulls
df.describe()         # basic statistics

df.isnull().sum()     # count missing values
df.dropna()           # or df.fillna(value)
df.duplicated().sum() # check for duplicates
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1000 entries, 0 to 999
    Data columns (total 13 columns):
     #   Column              Non-Null Count  Dtype         
    ---  ------              --------------  -----         
     0   Transaction ID      1000 non-null   object        
     1   Customer Name       1000 non-null   object        
     2   Email               1000 non-null   object        
     3   Product Category    1000 non-null   object        
     4   Product Name        1000 non-null   object        
     5   Quantity            1000 non-null   int64         
     6   Price per Unit ($)  1000 non-null   float64       
     7   Total Amount ($)    1000 non-null   float64       
     8   Payment Method      1000 non-null   object        
     9   Purchase Date       1000 non-null   datetime64[ns]
     10  Customer State      1000 non-null   object        
     11  Customer Age        1000 non-null   int64         
     12  Gender              1000 non-null   object        
    dtypes: datetime64[ns](1), float64(2), int64(2), object(8)
    memory usage: 101.7+ KB
    




    0




```python
# Display the top 10 rows of Dataset
print(df.head(10)) 
pd.set_option('display.width', 200)
```

                             Transaction ID        Customer Name  \
    0  eaae3c89-6fa6-48cd-8995-7b53c59af54a  Elizabeth Underwood   
    1  5cc5f6fa-0057-4331-9eac-ed0be9091ac6     Elizabeth Deleon   
    2  b4dad897-5e19-4aae-bc0d-d58c6695795a         Lori Morales   
    3  2a652c8c-0da3-4400-9a2e-1a361f1a9260          Ariana Yang   
    4  90338711-2f42-412b-90c1-ce27cfefe941       Carolyn Martin   
    5  b2e65b75-ae32-4c9d-82d8-176aba9efe98       Bryan Robinson   
    6  f205ec1f-56c6-4217-a99d-db26bb4f6c4b     Douglas Mcmillan   
    7  3db44d48-b589-4e0d-bad9-855031738a2f           Jay Bryant   
    8  d94d7122-86d6-4fce-8111-ad62d7bf7fd6            Derek Kim   
    9  09bdd4cb-6dec-4e36-bcc4-8ca48bda0f6a         Raymond Boyd   
    
                                   Email Product Category Product Name  Quantity  \
    0    robertjackson@golden-wilcox.biz      Electronics         Sign         4   
    1          timothycooper@hotmail.com           Beauty        Check         4   
    2                 eric25@hotmail.com             Toys     Congress         3   
    3      jacqueline23@salazar-ware.com        Groceries         Such         3   
    4            escobarjoseph@yahoo.com         Clothing     Everyone         1   
    5  hudsonpamela@swanson-williams.com           Beauty          Bar         3   
    6                   dawn49@gmail.com           Beauty        Third         2   
    7             paceamanda@hotmail.com           Sports         Site         1   
    8                 jeremy77@gmail.com        Groceries     Computer         2   
    9         ashepherd@newman-lewis.com           Beauty       Speech         5   
    
       Price per Unit ($)  Total Amount ($) Payment Method Purchase Date  \
    0              470.38           1881.52    Credit Card    2025-03-03   
    1                8.37             33.48     Debit Card    2025-01-05   
    2              489.66           1468.98    Credit Card    2024-10-06   
    3              209.93            629.79           Cash    2025-01-30   
    4                7.92              7.92    Credit Card    2024-05-27   
    5              226.85            680.55    Credit Card    2024-11-07   
    6              309.17            618.34     Debit Card    2024-12-28   
    7              267.72            267.72         PayPal    2024-05-20   
    8              414.04            828.08     Debit Card    2025-02-28   
    9              149.80            749.00         PayPal    2024-08-10   
    
      Customer State  Customer Age  Gender  
    0       Illinois            69    Male  
    1       Illinois            34    Male  
    2       Illinois            35  Female  
    3   Pennsylvania            18    Male  
    4        Florida            39   Other  
    5        Florida            48   Other  
    6        Florida            18    Male  
    7       Illinois            57  Female  
    8        Georgia            45  Female  
    9        Georgia            51    Male  
    


```python
print(df.to_string())
```

                               Transaction ID              Customer Name                                      Email Product Category   Product Name  Quantity  Price per Unit ($)  Total Amount ($)  Payment Method Purchase Date Customer State  Customer Age  Gender
    0    eaae3c89-6fa6-48cd-8995-7b53c59af54a        Elizabeth Underwood            robertjackson@golden-wilcox.biz      Electronics           Sign         4              470.38           1881.52     Credit Card    2025-03-03       Illinois            69    Male
    1    5cc5f6fa-0057-4331-9eac-ed0be9091ac6           Elizabeth Deleon                  timothycooper@hotmail.com           Beauty          Check         4                8.37             33.48      Debit Card    2025-01-05       Illinois            34    Male
    2    b4dad897-5e19-4aae-bc0d-d58c6695795a               Lori Morales                         eric25@hotmail.com             Toys       Congress         3              489.66           1468.98     Credit Card    2024-10-06       Illinois            35  Female
    3    2a652c8c-0da3-4400-9a2e-1a361f1a9260                Ariana Yang              jacqueline23@salazar-ware.com        Groceries           Such         3              209.93            629.79            Cash    2025-01-30   Pennsylvania            18    Male
    4    90338711-2f42-412b-90c1-ce27cfefe941             Carolyn Martin                    escobarjoseph@yahoo.com         Clothing       Everyone         1                7.92              7.92     Credit Card    2024-05-27        Florida            39   Other
    5    b2e65b75-ae32-4c9d-82d8-176aba9efe98             Bryan Robinson          hudsonpamela@swanson-williams.com           Beauty            Bar         3              226.85            680.55     Credit Card    2024-11-07        Florida            48   Other
    6    f205ec1f-56c6-4217-a99d-db26bb4f6c4b           Douglas Mcmillan                           dawn49@gmail.com           Beauty          Third         2              309.17            618.34      Debit Card    2024-12-28        Florida            18    Male
    7    3db44d48-b589-4e0d-bad9-855031738a2f                 Jay Bryant                     paceamanda@hotmail.com           Sports           Site         1              267.72            267.72          PayPal    2024-05-20       Illinois            57  Female
    8    d94d7122-86d6-4fce-8111-ad62d7bf7fd6                  Derek Kim                         jeremy77@gmail.com        Groceries       Computer         2              414.04            828.08      Debit Card    2025-02-28        Georgia            45  Female
    9    09bdd4cb-6dec-4e36-bcc4-8ca48bda0f6a               Raymond Boyd                 ashepherd@newman-lewis.com           Beauty         Speech         5              149.80            749.00          PayPal    2024-08-10        Georgia            51    Male
    10   cef3eb3c-76b5-4788-9987-3672194b6672                Ryan Murphy                           mary79@gmail.com      Electronics           Bill         2               45.36             90.72            Cash    2025-04-15        Florida            49  Female
    11   cbbf6ef5-a31d-4c7d-9613-ee5f26e6ec56                Angel Myers                       parkhannah@gmail.com           Beauty          Shake         5              395.58           1977.90          PayPal    2025-03-17        Florida            38    Male
    12   276b9874-ff0e-4f66-a7af-1e42e23ad4e1               Wendy Ingram                 rodriguezsarah@burnett.com       Automotive        Involve         3              492.85           1478.55            Cash    2025-01-21          Texas            50   Other
    13   76df017d-691f-47d2-9bb7-0b2c018fec08              Stephen Reyes           mccoyjennifer@jordan-ballard.net           Sports            Bar         5              348.00           1740.00      Debit Card    2025-02-20           Ohio            20   Other
    14   b2322721-4c0e-4f40-a991-5aa7db93fccf                Lisa Dorsey               veronicasimpson@gonzalez.com             Home        Soldier         2               96.15            192.30     Credit Card    2025-05-01        Florida            24   Other
    15   33aab27f-65c3-4484-8fb0-b57a04eb9f24             Edward Rollins                   robertslance@hotmail.com      Electronics         Better         2              415.23            830.46     Credit Card    2024-10-13        Georgia            32  Female
    16   8e30c724-5ce9-47f8-a224-40fe6f2e4a74            Becky Middleton                        waynegray@smith.com         Clothing           Upon         3               23.20             69.60  Mobile Payment    2024-06-27   Pennsylvania            60  Female
    17   e78e4f0b-a100-4139-b410-f016e7acd196                 Brian Long                  williamsrobert@miller.com             Home            Fly         4              232.29            929.16      Debit Card    2024-09-30     California            39   Other
    18   10ad0980-e9e3-4329-9f5c-ed4df7536c8d           William Richards                     barbarareese@yahoo.com         Clothing      Condition         2              350.57            701.14      Debit Card    2024-12-03          Texas            61  Female
    19   3eb2f49b-4df6-40de-8b0b-a17912610f33             Melissa Miller                  valdezelizabeth@scott.com      Electronics        Manager         4              201.65            806.60  Mobile Payment    2025-01-19        Georgia            24    Male
    20   4ddf2ca2-c6c7-4bba-aae3-5bae4da3e9fd                 David Diaz                       brittney25@frank.com           Sports   Relationship         4              474.52           1898.08  Mobile Payment    2025-04-09          Texas            52    Male
    21   d4612379-4393-4930-8444-4711dab708e8             Andrew Flowers                           bobby50@sims.com         Clothing           Easy         5              213.01           1065.05            Cash    2025-03-03           Ohio            38    Male
    22   e80c89bc-a3ea-49c5-862e-5cf4e677223f            Christopher Cox                        zharrison@yahoo.com           Beauty          Until         2              429.62            859.24            Cash    2025-01-30        Florida            65    Male
    23   c3049fa4-cb06-4d1c-a1c7-91e593c8fdc2                Steven Cook                         sbrown@hotmail.com      Electronics         Assume         5              259.82           1299.10      Debit Card    2024-06-13        Georgia            19  Female
    24   b24ee2a2-8f7c-453a-82f5-1fa2d7d4db66                Jean Fisher        ericjohnson@mcdaniel-richardson.com           Sports       Together         5               34.46            172.30          PayPal    2024-10-02           Ohio            62   Other
    25   8883abcf-641a-4ae3-83cd-cb83fdb8b8bf                 Stacy Reed                    edwardowens@hotmail.com        Groceries         Likely         4              163.36            653.44  Mobile Payment    2025-04-27       Illinois            38  Female
    26   9f10a016-7baa-4ffb-8bff-990885a8279b             Maurice Nelson                     jonathan93@hotmail.com             Home           City         1              179.07            179.07      Debit Card    2024-11-16   Pennsylvania            33   Other
    27   84f29438-b780-4747-a15e-9c78db8d0ec0                 April Mata                  mitchellrichard@gmail.com       Automotive           Data         4              259.50           1038.00      Debit Card    2024-05-11          Texas            23    Male
    28   5a6ede65-19d0-43b1-b860-3abedb25f4da                 Dale David                          craig57@jones.net             Home           More         4              496.62           1986.48            Cash    2025-01-25       New York            61  Female
    29   729fb317-7a91-4de5-aa53-5c4a4c21f8e5           Tracy Washington                     tammysmith@hotmail.com      Electronics           Town         5              210.47           1052.35  Mobile Payment    2025-04-06   Pennsylvania            22    Male
    30   2c254030-ec0f-4a66-941c-f4033eed28ea              David Johnson                   garnerthomas@hotmail.com         Clothing           Stay         1               94.35             94.35  Mobile Payment    2024-07-04          Texas            60    Male
    31   82d85d8b-781e-4f69-af55-a04c749eab25            David Zimmerman                       yschwartz@ingram.org           Beauty       Election         4               35.30            141.20          PayPal    2025-04-18       New York            70  Female
    32   b0a275b2-9b1d-4b21-b2e5-74f8f4cf8b4c              Joseph Rivera                     jerryrobbins@yahoo.com             Toys          Cover         1              324.37            324.37            Cash    2024-11-14        Georgia            56  Female
    33   032250ec-e475-4387-aaa9-9454df880fa4                Paul Zuniga                 wilsonpriscilla@brewer.com        Groceries          Maybe         3               15.78             47.34  Mobile Payment    2024-09-02        Florida            68   Other
    34   a62b9bf8-aebf-4a3f-a99f-50480cc1248f              Hector Lawson                    martineznorma@gmail.com      Electronics       Shoulder         3              111.54            334.62            Cash    2024-08-12       New York            68  Female
    35   cad5e95c-6f82-4bad-8e40-cb8474a83aa4                 Cory Logan                      morrisangel@gmail.com           Beauty         Finish         1              246.41            246.41      Debit Card    2024-05-02     California            27   Other
    36   45fba049-0121-447d-a8be-f477d40954cd               Haley Moreno                          paige95@gmail.com       Automotive           Item         4              427.84           1711.36      Debit Card    2024-08-08        Georgia            29  Female
    37   e1a07879-fc8e-4729-9597-b80cad3f1756          Shannon Rodriguez                    heathersims@carroll.com        Groceries        Student         1              126.76            126.76      Debit Card    2024-07-02        Georgia            19    Male
    38   8493e93a-b974-4773-b8ed-b2555c672f5b             Tracey Fuentes                 johnsonshane@chen-lee.info         Clothing       Anything         4              440.84           1763.36  Mobile Payment    2024-12-02           Ohio            57    Male
    39   a1cc4d1a-527f-486e-b76e-08047c781a53                Susan Patel                         pamela49@yahoo.com             Home          Peace         5              221.57           1107.85            Cash    2024-09-17       New York            64   Other
    40   599f858b-273c-4f0b-b396-2b273e1f195e                 Jason Cobb                          anita28@gmail.com         Clothing          Throw         5                8.55             42.75     Credit Card    2025-02-13        Georgia            43  Female
    41   98b671de-f90a-451a-8fd6-a6402429e955              Russell Lopez                      carterstuart@long.com             Home       National         5              449.20           2246.00      Debit Card    2024-05-15           Ohio            49   Other
    42   fa38a901-96ab-4f75-9038-8d906f41a673        Christopher Sanchez                        mwalker@preston.com             Toys        Someone         2              367.06            734.12     Credit Card    2024-10-05   Pennsylvania            33  Female
    43   aefd7686-7eab-4362-bb2c-35c276353364               Robert Davis            wileychristopher@mclaughlin.com           Sports           Word         5              284.97           1424.85            Cash    2024-11-08        Georgia            48   Other
    44   3181d176-1a80-4bba-8938-1fd25f4bd013                Adam Harper                     emilyscott@hotmail.com       Automotive         Others         1              125.26            125.26          PayPal    2024-07-09     California            23   Other
    45   81276fb3-c22f-41f6-ba3a-a6997929248e            Jeremiah Watson                          wbarnes@yahoo.com           Beauty            Air         3              131.36            394.08  Mobile Payment    2025-02-01           Ohio            19    Male
    46   c67fd490-ea76-42b4-b8c5-f37a2dfe545e                Jesse Lewis                 kpowers@mason-arellano.org         Clothing          Think         5              198.63            993.15  Mobile Payment    2024-08-22     California            61  Female
    47   ce97132c-82ad-41d1-b6d8-52ad459d2370             Daniel Mcgrath                          rhill@johnson.com        Groceries          Mouth         5              413.85           2069.25      Debit Card    2025-01-02       Illinois            41  Female
    48   917286c5-b7bf-4236-a04c-6de4ec4c6a5b            Richard Higgins                          debra86@gmail.com      Electronics       Identify         3              303.52            910.56     Credit Card    2024-07-22          Texas            52   Other
    49   869088d6-6dd2-4aae-8625-6d4b041ab465           Latoya Alexander                     jeanette81@pearson.com             Toys         Future         3              214.64            643.92  Mobile Payment    2024-10-26     California            32    Male
    50   73a3d608-2311-410f-a827-0c5770262d65           Christopher Shaw                andersonheather@allison.com      Electronics     Experience         2              166.71            333.42          PayPal    2024-06-03           Ohio            55  Female
    51   5508e748-06c4-4f55-9316-52a9a2fd1753               Ryan Johnson          christiegonzalez@murphy-patel.com      Electronics       Probably         1              337.57            337.57     Credit Card    2024-05-31       New York            67   Other
    52   66048ae0-7716-4c67-be9e-c623bb859c92               Judith Ayers                      omeadows@carrillo.com           Beauty         Factor         4              186.15            744.60            Cash    2024-06-06       New York            34    Male
    53   8d8d7175-e6b7-403f-8310-e7bc89302d64            Kimberly Garcia                          gomezlisa@ray.com           Sports          Whole         1               12.14             12.14      Debit Card    2024-12-16       New York            18  Female
    54   ab2616bf-1509-4cfd-be81-4faa94710b5e               Gary Andrade                   tonyholloway@hotmail.com        Groceries         Person         4              221.39            885.56      Debit Card    2024-05-05     California            30    Male
    55   cde11354-611b-4496-8265-fbc3710bd462            Mariah Williams                       audreybeck@allen.org       Automotive           Size         5              188.34            941.70     Credit Card    2024-07-14        Florida            61   Other
    56   0edd0284-b589-4ae0-ab59-6eca40cab639              Peter Johnson                       craigdean@reeves.biz         Clothing         Minute         5              332.90           1664.50            Cash    2025-04-01       New York            44    Male
    57   a2d0da96-3b86-43d7-a52e-4e4fd97c8d0f               Phillip Webb                  fowlercourtney@parker.org       Automotive           Wife         1              212.34            212.34     Credit Card    2024-12-06     California            46    Male
    58   7b1aa4cc-be3d-4249-ab9d-7574234b8508              Antonio Perez                    greenbrittany@yahoo.com           Sports            Try         2              434.68            869.36            Cash    2024-07-01       Illinois            52    Male
    59   c99e2bc8-d157-441a-800d-3bfb4175a62d                Kara Thomas              adamnguyen@briggs-fisher.info       Automotive       Painting         1              450.70            450.70          PayPal    2025-03-11       Illinois            58  Female
    60   ef156fd5-98e3-4d30-bf16-5bf4cb8cc460           Jillian Robinson                       nguyenemma@yahoo.com         Clothing      Establish         4              125.16            500.64            Cash    2024-07-01        Georgia            57  Female
    61   ed9a35e4-2d14-43b8-9f4b-f25249177ea4                  Laura Lee                      stephen45@hotmail.com         Clothing             At         3              462.60           1387.80            Cash    2024-10-10        Florida            30   Other
    62   447dfae0-b388-4d85-a837-70f92d3d7738              Adrian Watson                  dianelawrence@hotmail.com           Beauty       Daughter         2              216.22            432.44     Credit Card    2024-11-07     California            36    Male
    63   d43afbd8-ca89-4590-af24-21bc8ce3b181           Dr. Richard Ward                eric37@morales-erickson.com           Beauty         Former         2               12.44             24.88     Credit Card    2024-11-09          Texas            33   Other
    64   61bdb820-acea-4cf7-b738-e019caa012e3               Brian Thomas                    thompsonjames@booth.com        Groceries           Than         3              430.67           1292.01     Credit Card    2024-10-09       New York            34  Female
    65   d4c42edc-2118-4cb9-824f-2c38b703fd86              Jennifer Wood                         rjohnson@smith.biz         Clothing        Explain         2              352.62            705.24          PayPal    2025-04-13        Florida            20    Male
    66   8abefb37-cbb1-4b8e-8d70-873003700423                Dean Turner               cristinarichmond@hotmail.com             Toys          Stage         4              284.56           1138.24     Credit Card    2025-01-19        Georgia            35  Female
    67   bf81eb87-8441-4387-a4f6-2c2dce2166a9           Christine Watson                   kerri06@thomas-smith.com           Sports       Recently         2              483.19            966.38     Credit Card    2024-10-08          Texas            40   Other
    68   c82dd749-9402-4bff-9686-51f4b6f3215c             Jeffrey Wilson                    lori63@fritz-miller.com        Groceries           Fish         2              173.68            347.36     Credit Card    2024-11-13           Ohio            40    Male
    69   90022c45-5551-4513-a98d-eedb4799b65c          Patricia Harrison                        michael08@gmail.com        Groceries          Focus         4              442.62           1770.48     Credit Card    2025-03-25        Georgia            30    Male
    70   f1c55dbc-67d0-4228-8f75-6847dab4e14b              Jesus Mullins                         sbrown@hotmail.com      Electronics        Address         3              296.20            888.60     Credit Card    2024-08-23     California            55    Male
    71   b8d50ddf-750f-4e56-86ec-4e2eaad9a8d5                 Tara Moore                 kimberlymarshall@bauer.biz             Toys            Say         5              265.57           1327.85      Debit Card    2024-07-09       Illinois            57   Other
    72   f255b803-8423-4028-98c8-81c09556dbb7             Carrie Mullins                    russellkristy@gmail.com             Toys           Main         2              219.90            439.80            Cash    2024-09-26        Florida            43   Other
    73   8e759e84-eb87-4c9b-b163-c271ee47ae23               Tonya Taylor                      megannelson@gmail.com             Toys            Way         4              293.85           1175.40          PayPal    2024-10-05        Florida            57    Male
    74   8462fd51-2f61-44bd-8f20-0633f0bf238e                  Jill Tran                  donaldstanley@hotmail.com       Automotive           Main         2               72.71            145.42          PayPal    2024-05-14       New York            49  Female
    75   e7d6b75a-b50d-45ab-90b0-3f82cff999e4                Gina Walton                monicakennedy@henderson.com       Automotive         Happen         4              473.64           1894.56          PayPal    2024-09-26           Ohio            52    Male
    76   a966b337-455b-485a-8e56-40422dd86731             Joshua Johnson                    phillipgarcia@gmail.com             Home         Author         5              126.54            632.70      Debit Card    2024-07-10     California            67   Other
    77   1b998795-dd00-4504-a4af-76f6bd471e71             Danielle Roman                   cdavis@hernandez-ray.com             Home         Suffer         4              133.65            534.60            Cash    2025-02-10        Georgia            40   Other
    78   3e87d290-378c-4c3f-83ce-43957a98bf8e          Mrs. Abigail Cook                         eshannon@gmail.com             Home           Each         3              262.84            788.52      Debit Card    2024-07-29     California            20    Male
    79   d9e0e273-8af1-4f2e-b7cc-84c110cf10de             Jessica Stokes                    cindygarcia@hotmail.com         Clothing        Million         4              200.31            801.24            Cash    2024-05-17        Florida            18  Female
    80   e9511a47-f9c1-40a1-850f-bdf59c2f7e6e                Eric Sutton                 andraderebecca@russell.com           Sports          Exist         1              456.42            456.42  Mobile Payment    2025-02-25       Illinois            58   Other
    81   76a28e50-f33b-4de9-a735-9ea10a167f1b               Marie Mclean               rodriguezjessica@hotmail.com       Automotive          Story         2              177.53            355.06  Mobile Payment    2025-01-07       New York            64  Female
    82   8dc5f355-b245-4c8f-b8e9-d3e243cea536                Tracy Lewis                  tiffanywilliams@mccoy.com      Electronics         Future         3              139.50            418.50      Debit Card    2024-06-02   Pennsylvania            47   Other
    83   0431648e-b06e-4e7c-a6af-bcc7182441b0                 Jason Todd                        pbutler@hotmail.com       Automotive        Reflect         1              135.72            135.72          PayPal    2025-01-31           Ohio            57   Other
    84   2e8b3756-7814-45c8-8516-8e43e0344287           Jacqueline Owens                         rachel89@yahoo.com             Toys           Fact         2              431.71            863.42          PayPal    2024-09-01     California            31    Male
    85   a74c8dd0-fd8c-4fd2-b7e9-5cc09efbc39b           Jennifer Johnson                       rebecca46@larson.com        Groceries          Heavy         2              253.18            506.36      Debit Card    2024-07-05   Pennsylvania            63   Other
    86   de442186-78dd-4dc7-b912-17d286ff0041               Daniel Baker                      fredrosales@yahoo.com       Automotive        Mention         4              418.46           1673.84      Debit Card    2024-12-22        Georgia            49   Other
    87   cfc7435d-7cad-4386-b01f-6b37508edabd            Joseph Gonzalez                          aaron49@gmail.com      Electronics           Team         4              129.22            516.88     Credit Card    2024-10-04           Ohio            67    Male
    88   92c39923-4091-4e10-8e47-96bb1b0cb37d               Anita Castro                        melissa41@weeks.com        Groceries        Improve         5               88.16            440.80     Credit Card    2024-10-20        Florida            70  Female
    89   1d74197d-26f4-4e00-b41a-f89c62bdb7e6                    Rita Ho                      blackrobert@yahoo.com             Toys      Character         4              198.50            794.00     Credit Card    2025-03-28     California            63    Male
    90   28fb85c5-3052-4898-a53e-4e215fa9b0e4           James Richardson                      joycealexis@yahoo.com      Electronics            Gun         3              268.88            806.64          PayPal    2024-08-18        Florida            65  Female
    91   27019ae7-7164-4faa-b1e5-89f34a63e0a3                Amanda Reid                         amanda66@gmail.com       Automotive       Although         1               19.75             19.75  Mobile Payment    2024-09-03     California            54    Male
    92   add7d582-b5f3-4eb6-875d-f54fb0c67dca               Debbie Young               frederickkatherine@yahoo.com           Sports           More         4              252.64           1010.56  Mobile Payment    2025-04-28     California            50   Other
    93   565f8baf-fb07-4f72-a080-69b721c8235e               Timothy Hunt                      bowenandrew@diaz.info       Automotive            Car         4              394.12           1576.48      Debit Card    2024-06-09        Georgia            63    Male
    94   59597012-0b5c-487f-b41b-44b4968990b5               Casey Graham                 sromero@martinez-hall.info             Home        Develop         3              149.59            448.77      Debit Card    2024-12-01          Texas            65    Male
    95   0b9bbe3f-198d-48c8-8e99-dcc6769cc89d               Cynthia Frye                       rschmidt@hotmail.com        Groceries        Despite         4               98.57            394.28          PayPal    2025-01-18       Illinois            26    Male
    96   a9a519d9-2086-4199-9c63-9a570e2f2c36            Joseph Martinez                           anna81@yahoo.com         Clothing         Answer         3               94.60            283.80            Cash    2025-02-09        Florida            19  Female
    97   4df32903-e01f-4390-b90d-1177df9fc1b2           Joshua Rodriguez                    kingstephanie@gmail.com             Toys          Story         3              416.98           1250.94     Credit Card    2024-08-11     California            55  Female
    98   953226af-6ab8-491e-9c37-ad7b2d075b8c               Jillian Frey                      robert33@salinas.info         Clothing           Then         2              305.12            610.24     Credit Card    2024-07-15          Texas            43  Female
    99   1f5d4b92-53c8-4fc1-beaa-372320d5b11c                Tammy Jones                       janice02@hotmail.com           Beauty         Budget         5              297.93           1489.65     Credit Card    2024-10-24          Texas            39   Other
    100  c0b86471-2cf7-4024-b022-fd901bdd2b4a           Matthew Phillips                       kimberly19@gmail.com           Beauty            Him         3              107.43            322.29      Debit Card    2024-06-12           Ohio            33   Other
    101  fb66220e-3ddb-4e4f-a901-ed4afe9256d5            James Gutierrez                       markrivera@yahoo.com           Sports        Respond         1               70.65             70.65      Debit Card    2024-08-14       Illinois            44  Female
    102  80c823b4-501f-42c3-9ea4-71168d00c756             Heather Jacobs             wheelercaitlin@jones-davis.biz             Toys            Low         2              154.92            309.84          PayPal    2025-01-27          Texas            61    Male
    103  bf32eb41-8158-4ebf-a8cb-c02036a54877             Nathan Hampton                         mjones@hotmail.com         Clothing           Free         4              123.79            495.16  Mobile Payment    2024-06-05        Florida            41  Female
    104  3f0578af-cb9e-44e8-9385-d1cd59f7660c           Marilyn Robinson                  andrewrodriguez@lopez.org           Sports          Image         2                7.22             14.44  Mobile Payment    2025-01-05          Texas            56  Female
    105  5aba9f9c-2d77-419b-aa4b-21d61fbe806e            Kyle Pennington              nicholas79@richards-davis.com       Automotive         Career         4              255.04           1020.16  Mobile Payment    2024-05-05       New York            42    Male
    106  a6240a9a-b6b1-48c4-91b8-996e6131f052                 John Young                       hdavis@rodriguez.com             Home        Control         5               18.96             94.80            Cash    2025-04-26          Texas            57   Other
    107  6bcbed76-a739-4ebe-99d3-07e2c47b0e57              David Pacheco                  kristavazquez@hotmail.com       Automotive          Stage         1              246.15            246.15          PayPal    2024-12-21        Florida            47    Male
    108  00dc9475-1a71-4cfe-b0c3-7257ecf9ad40           Darren Wilkerson                          osparks@yahoo.com        Groceries       Material         1              390.62            390.62  Mobile Payment    2024-09-21        Georgia            54    Male
    109  e4a658c3-b402-454b-a3b7-5bd83205876f          Jermaine Martinez                      jordanamanda@pace.com             Toys         Writer         1              148.49            148.49  Mobile Payment    2025-01-27     California            62  Female
    110  9c0e2358-1160-4b9f-a64c-6be96c3f8d3b              Brett Mcclain                      dwilliams@hotmail.com         Clothing           Foot         3               21.14             63.42  Mobile Payment    2025-04-02           Ohio            19   Other
    111  80ea104e-d72d-4576-8b20-59212e6f8aa5                Steven Hunt               blackmark@west-daugherty.com         Clothing          Black         1              144.63            144.63            Cash    2024-06-07           Ohio            46  Female
    112  bf34d208-3cc2-4941-90ad-c9212be899e2           Kristin Martinez                     susanfreeman@yahoo.com        Groceries          Seven         4              226.11            904.44  Mobile Payment    2025-02-25        Georgia            67  Female
    113  84b928b7-5f2e-4bff-aa47-97d0b50d995e            Michael Simmons                  williamsstacy@hotmail.com         Clothing         Second         2              228.50            457.00            Cash    2025-02-13       New York            27  Female
    114  c62da601-d3e8-4766-8b88-97db36a049c9           Maureen Mcintosh                          pflores@yahoo.com         Clothing           Nice         4              122.15            488.60      Debit Card    2024-06-15     California            23  Female
    115  4d317f16-b2a8-4275-960f-d43b164bc871               Chad Watkins                       bellhannah@gmail.com      Electronics          Adult         3              245.08            735.24      Debit Card    2024-12-07           Ohio            32  Female
    116  08404646-4270-4cb0-90e6-e7157d30918c             Thomas Johnson                       rachel36@barnes.info           Beauty        Hundred         2              496.56            993.12          PayPal    2024-05-06          Texas            58    Male
    117  f9ed0194-aa55-459c-9b99-b72dd0e01e17              Hunter Dennis                        doyleeric@gmail.com       Automotive            Let         1              215.00            215.00          PayPal    2024-10-31        Georgia            66    Male
    118  8d41a8d5-d554-4587-b2a9-9158473490dd               Brent Barnes                   stewartjesse@hotmail.com             Toys         Indeed         1              177.15            177.15     Credit Card    2024-11-23     California            59    Male
    119  db666ea1-94ef-41a1-a61a-4b6f3e35c4f9                Tony Chavez                     trevormolina@smith.org      Electronics         Player         4              267.81           1071.24     Credit Card    2025-04-27        Florida            68    Male
    120  8d396d8b-4dbe-4685-8224-6b888049187c                Chad Rogers                           rkelly@perez.net           Sports           Hand         5                5.45             27.25            Cash    2024-12-14   Pennsylvania            51    Male
    121  323e53ea-019a-4a0c-b31d-350b495c612d               Joseph White                         luis03@hotmail.com         Clothing           Well         5              456.16           2280.80  Mobile Payment    2024-07-07       Illinois            37  Female
    122  ed0f245a-30a1-4179-bbec-343f4676481e               Patrick Khan                          jmiller@gmail.com      Electronics          Table         2              151.12            302.24      Debit Card    2024-11-11   Pennsylvania            48  Female
    123  596d17b1-f56c-4ab8-83d3-2936e78f646d                 Ronald Kim                       lawrence01@young.com       Automotive         Record         5              376.23           1881.15     Credit Card    2024-09-11       New York            50  Female
    124  858f85d8-0214-4521-b059-9ea69374519f                 Kyle Scott                  palmeralexander@yahoo.com           Sports         Strong         3              495.21           1485.63            Cash    2024-10-24        Georgia            39   Other
    125  99d76884-4b3b-4a7f-ab6e-9383d6b4195d               Carmen Smith                bradfordjennifer@gibson.com       Automotive          Admit         3              123.83            371.49  Mobile Payment    2025-04-29           Ohio            49   Other
    126  a6323417-c326-46f4-82d0-7c71efc234a0              Beverly Silva                     lopezstephen@gmail.com             Toys          World         1              319.92            319.92      Debit Card    2024-12-22          Texas            19  Female
    127  e63ca7fb-1606-41a2-af6b-f4ea250f31ad                 John Baker                   kimberlybutler@yahoo.com           Beauty       Position         5              294.39           1471.95  Mobile Payment    2025-03-26           Ohio            59  Female
    128  85f3f5f2-a753-409f-8d4d-ca61e014af77            Melissa Navarro                       michelle32@burns.com      Electronics        Soldier         5              394.60           1973.00      Debit Card    2024-11-10           Ohio            62    Male
    129  4149f378-6595-4cbc-b50e-6abed84520e2               Holly Finley                   donaldgonzalez@gmail.com         Clothing          Close         2              305.47            610.94  Mobile Payment    2024-09-27       Illinois            66    Male
    130  1dddc141-e1bc-4613-8de8-40650846d913              Chase Herrera                      fmason@montgomery.com         Clothing        Explain         1              409.71            409.71            Cash    2024-09-03   Pennsylvania            58   Other
    131  178d5c36-a53d-439f-b5c6-c30e20c3811f               Karen Dodson                     sarasullivan@gmail.com           Sports         Friend         3              437.06           1311.18          PayPal    2024-11-23     California            30  Female
    132  a9c566b5-b0cf-45f6-a47a-9875db556c07                Anna Watson                   collinstimothy@yahoo.com        Groceries             On         3              315.55            946.65      Debit Card    2025-01-28       Illinois            43  Female
    133  aed05593-49fd-47ef-8bb1-0a26b3e61160          Joshua Harrington                     charles01@shelton.info      Electronics             Of         4              196.10            784.40  Mobile Payment    2024-10-31       New York            24    Male
    134  5120c95a-bc3b-4b79-a967-b38abebc9de2              Stephen Avila                          omiller@yahoo.com           Sports        Capital         2              453.05            906.10      Debit Card    2024-06-15          Texas            47  Female
    135  7968d644-e0ff-4a8f-a5e6-e0e1e1ebc7c1            Pamela Shepherd                          craig48@gmail.com       Automotive            Car         2              260.24            520.48     Credit Card    2024-12-08       New York            20  Female
    136  5c95c4f6-1280-4686-b3f3-4fcf559e72bc           Ronnie Gutierrez                     larsonjohn@summers.com      Electronics           Very         3               74.56            223.68  Mobile Payment    2025-04-21       New York            56    Male
    137  eebfe7c2-e35b-472e-bf06-02503a3f3955              Richard Gomez                     lucerogeorge@gmail.com             Toys            Way         1              109.15            109.15            Cash    2025-03-01        Florida            63  Female
    138  87975cc8-0bd9-4273-9524-5625fa7275c8              Andrew Mathis                          jwalker@yahoo.com       Automotive         Worker         3              221.20            663.60          PayPal    2024-07-07           Ohio            45    Male
    139  a7c81222-f787-4e25-89b6-6f40c0410806               Jimmy Harper                  landerson@watts-price.com             Toys          Force         1              411.53            411.53      Debit Card    2025-03-03          Texas            20    Male
    140  b9109dc1-47e1-479f-afc6-11e763589f45             William Farmer                         ashley11@gmail.com      Electronics        Quality         2               21.35             42.70      Debit Card    2025-02-23           Ohio            69   Other
    141  3888024d-d256-4888-aeb7-190a49589cad            Sharon Williams                 brittanyrobinson@young.com        Groceries           Sure         4              110.67            442.68            Cash    2024-05-28          Texas            23    Male
    142  2c3c4840-b908-4a9a-85a0-135b30c7b29a           Brandon Harrison                   taylorreynolds@yahoo.com             Toys            She         5               15.72             78.60  Mobile Payment    2025-03-17          Texas            21   Other
    143  957944e9-b744-4a98-b557-466392ebee09          Cassie Peters PhD                       steven47@hotmail.com        Groceries         Degree         4              225.88            903.52      Debit Card    2025-03-05     California            62  Female
    144  6a341127-85eb-4c37-9d3d-6c5a3f2a61ec               Sarah Turner                        brandon73@gmail.com           Beauty       Recently         1              116.41            116.41     Credit Card    2025-02-26        Florida            62   Other
    145  2da074e7-f427-4197-8965-cd11bf5673ec          Christina Edwards                    gibsonemily@hotmail.com       Automotive           Keep         5              337.57           1687.85     Credit Card    2024-05-24          Texas            26  Female
    146  37f12d78-1b00-4406-8a69-7079080793b1                Sean Turner                    brownmariah@hotmail.com        Groceries           Soon         1              175.06            175.06            Cash    2024-09-23          Texas            51    Male
    147  6de42f3d-c2a4-4d3c-b338-abc87c1905bf              Kerry Collins                      patrick40@hotmail.com       Automotive      Difficult         5              243.73           1218.65     Credit Card    2024-06-13   Pennsylvania            20    Male
    148  f1752e06-1c45-4e23-8e2b-32debbf7e7b0           Kenneth Trujillo                 samanthalucas@martinez.com             Toys      Authority         5              155.75            778.75          PayPal    2024-10-12   Pennsylvania            33    Male
    149  740281f8-0224-4496-9d8a-4821751ec4ff              Nathan Austin                          ray63@watkins.com           Beauty       Movement         1              209.73            209.73      Debit Card    2024-08-25   Pennsylvania            26    Male
    150  2538656c-129a-49e3-b420-2a5b33bf4aa2               Cory Hawkins                  qhayes@stephens-quinn.com       Automotive           Once         1               51.67             51.67            Cash    2025-03-13     California            44  Female
    151  2039e8ff-768b-4a93-bcdb-952189573ce0              Heather Zhang                   esparzaerica@hotmail.com       Automotive         Figure         4               89.18            356.72     Credit Card    2024-11-03        Georgia            34    Male
    152  ec646432-386d-44fb-9410-f25df71c3926              Joseph Harris                         davidlee@gmail.com       Automotive         Really         3               88.41            265.23            Cash    2024-11-09       New York            61    Male
    153  1372324e-9127-4ec7-98ba-c8f22a60df5f               Larry Wright          colleenfrazier@burton-potter.info        Groceries           Blue         1               33.51             33.51          PayPal    2024-12-20        Georgia            44  Female
    154  615683f3-c8cd-4a35-b094-070f16fcf4fc               Gina Pearson                garciachristopher@gmail.com           Beauty          Stock         3              241.23            723.69          PayPal    2024-07-21        Georgia            69   Other
    155  97a9f7d5-16ae-4534-8d8d-567e1dbbc757               Maria Joseph             danielavila@robertson-king.com           Sports           Wind         3              123.21            369.63      Debit Card    2025-05-01       Illinois            70    Male
    156  4fff5a49-abc2-4d24-8592-dac53ea01373            Theresa Simpson                 nicoleunderwood@reeves.com           Beauty         Rather         1              437.00            437.00            Cash    2024-08-20       New York            42  Female
    157  cdadf7a5-641d-4834-b1d2-7ab615768195               Linda Powell                  carterbreanna@hotmail.com             Toys         Entire         1              224.80            224.80      Debit Card    2024-12-13       Illinois            67    Male
    158  4ec301bc-650c-424d-9a52-2470aecbdd76           Elizabeth Bowman                      rivaslauren@yahoo.com         Clothing         Threat         2              137.77            275.54      Debit Card    2025-03-31          Texas            27   Other
    159  fa036fca-4aef-4777-bd66-a229128b9c4a        Kristina Carter PhD                        melissa84@yahoo.com             Home          Trial         2              286.52            573.04     Credit Card    2024-06-03       Illinois            27   Other
    160  6ecafb55-6201-4d8a-8c07-dc55335bdb46            Brandon Kennedy         joannjackson@singleton-jenkins.com             Home          Civil         2               35.01             70.02  Mobile Payment    2024-07-08        Georgia            53    Male
    161  56b51760-50d7-49bd-9c94-a3ab9fd49437                 Julia Cobb                     marycastillo@gmail.com           Sports         Effect         3              344.34           1033.02  Mobile Payment    2024-10-07           Ohio            29    Male
    162  61740fba-9d6a-46ee-a9cd-fae6f13a4aa3           Michelle Gilmore                         joseph30@gmail.com         Clothing           Read         3              264.51            793.53  Mobile Payment    2024-07-12       Illinois            28  Female
    163  f822881d-9168-4a52-a183-18365718c1fc             Kayla Phillips                        ahorne@williams.com         Clothing            War         2               83.02            166.04            Cash    2025-03-07       New York            53   Other
    164  3f3c3f36-ec61-4364-8d1b-f282eaa77965                 Sara Avila                        garymack@fields.com         Clothing           Wide         4              277.82           1111.28          PayPal    2025-03-16   Pennsylvania            59    Male
    165  08a7e49e-bd94-4c3c-808e-21a73f33a068             Julia Franklin                           john54@gmail.com           Beauty           Some         3              198.90            596.70            Cash    2024-12-26     California            41  Female
    166  f30a5488-2eca-4351-854b-554b763f3f3a           Elizabeth Mercer                            psims@baker.com         Clothing           Sort         1              312.34            312.34          PayPal    2024-11-27          Texas            50    Male
    167  0f91cd2d-d098-4fb9-ba3d-52dc57043bdf               Marie Butler                           ahunter@kane.com         Clothing           Sign         1              241.04            241.04            Cash    2025-04-27          Texas            54  Female
    168  7acd435e-748e-4c00-a733-8863885fb26a                Donald Ward               kmiller@vargas-davidson.info             Toys            Ask         4              322.35           1289.40          PayPal    2024-07-06          Texas            63  Female
    169  ca2e4b43-b33e-4aa6-8075-78af1b43d833             Matthew Martin                    danielmoore@hotmail.com         Clothing            Job         5              179.26            896.30            Cash    2024-11-14   Pennsylvania            43  Female
    170  e632b762-919c-4421-a9e3-88adbcf73add              Bonnie Wagner                  katherinehowell@yahoo.com           Beauty             Pm         1              206.09            206.09            Cash    2024-07-19           Ohio            30  Female
    171  812188b4-3ae0-4671-a431-0c234c92259f             Kayla Mcdonald             adammcdaniel@solomon-small.com        Groceries           Left         2              383.38            766.76          PayPal    2024-07-31           Ohio            31    Male
    172  19c9c1cc-fbb6-4daa-9aac-2895175acd95        Christopher Barnett                     vanessajones@garza.com         Clothing           Take         3               62.74            188.22            Cash    2025-02-18       Illinois            47  Female
    173  82cdd670-43b8-4285-a8de-96e7270f1daf                Manuel Cobb                ashleyrodgers@rodriguez.com         Clothing             Of         5              436.97           2184.85          PayPal    2024-12-31          Texas            18   Other
    174  ec6e771e-fe46-4b22-9785-ff49ddee3a34              Matthew Heath                          kbecker@yahoo.com        Groceries           Move         4              143.01            572.04  Mobile Payment    2024-08-10        Georgia            37    Male
    175  efecddcc-6df7-40a3-a2f0-b43684e001d7          Samantha Harrison                    rogersjamie@hotmail.com             Toys        Protect         2              381.11            762.22  Mobile Payment    2025-03-29        Georgia            23  Female
    176  af89bdee-1b2e-4419-82f1-acaa43297261            Tyler Mccormick                       uthompson@morgan.com           Beauty        Project         1              223.87            223.87     Credit Card    2024-08-29          Texas            22   Other
    177  a40a6a60-7f11-4271-99e0-da781d819228            Danielle Joseph                     bettygregory@gmail.com             Toys          Hotel         1              255.89            255.89  Mobile Payment    2024-08-03        Florida            46    Male
    178  aeac52b0-be7d-44e5-ab9a-3dd341cd7ac0            Leslie Robinson                      solissharon@brown.com        Groceries            Now         5              334.20           1671.00  Mobile Payment    2025-04-03           Ohio            23  Female
    179  d2331a8b-2ebe-4a44-8222-a23edb0f7884         Nicholas Mccormick                       josephward@gmail.com           Sports         Always         5              439.97           2199.85            Cash    2024-05-23          Texas            53   Other
    180  55ac7781-3c73-40e7-876c-21430d69059e             Keith Cardenas                         mmora@williams.com           Sports           Task         5              152.24            761.20            Cash    2025-01-01        Georgia            42   Other
    181  4e4c205b-4592-4da1-86b0-f4ba9f890cea                 Mark Roman                      cmclaughlin@yahoo.com       Automotive       National         3              259.97            779.91          PayPal    2024-11-08     California            21    Male
    182  4c5ea896-5694-4974-a8ed-130b2c563a76              Lauren Walton                ryan15@johnson-petersen.biz         Clothing         Degree         3              359.78           1079.34            Cash    2024-07-03     California            60  Female
    183  61663037-e47d-4a4f-a52a-d6ada68e2eb1             Jimmy Reynolds          josedickerson@thompson-stark.info       Automotive            Kid         3              394.67           1184.01            Cash    2025-01-14       Illinois            29    Male
    184  da80d82d-aa5b-4854-8870-20d47b2ac229            Alexander Petty                      bryantdavid@gmail.com           Beauty         Decade         1              272.02            272.02            Cash    2024-08-07       Illinois            34    Male
    185  f227cd92-462a-4edc-9eac-5249e789563f              Logan Kennedy                       andrew01@hotmail.com       Automotive         Ground         2              259.82            519.64      Debit Card    2024-08-01        Georgia            47   Other
    186  3be18e7b-225d-4261-968c-f4c102317ef3            Jennifer Howard                        ggonzalez@yahoo.com         Clothing       Together         3              188.57            565.71          PayPal    2025-01-14           Ohio            36  Female
    187  ca515d44-4e29-432b-b172-eb175b44fc42            Andrea Anderson                           tony75@gmail.com           Beauty     Investment         2              361.75            723.50     Credit Card    2024-12-30       New York            69   Other
    188  0f4581e9-af3a-4a56-9ae0-4b1bd029835c                 Rodney Lee             vincentamy@harris-marshall.com      Electronics          Sound         2              461.28            922.56  Mobile Payment    2024-07-26     California            64  Female
    189  667c2f50-7cc5-42e7-ab2c-c78aa1795bca             Steven Jackson                       wsampson@hotmail.com             Home         Public         3              100.45            301.35      Debit Card    2024-08-19           Ohio            57  Female
    190  41060502-bd21-44d6-97a9-79fb04bd9d32             Tricia English                stephaniebeasley@carter.com             Toys         Little         5              374.58           1872.90          PayPal    2025-01-07       Illinois            18  Female
    191  689604b9-c958-4af0-b4f4-0d658b78d207               Tammy Duncan                      sharonhenry@gmail.com           Beauty            Its         3              308.37            925.11      Debit Card    2025-01-31        Georgia            25    Male
    192  089fdfb0-6360-459d-84fd-b19cba98715b           Barbara Crawford                    brianmckenzie@gmail.com        Groceries        Current         5              158.81            794.05  Mobile Payment    2024-12-16        Florida            60   Other
    193  c6c68aca-80d6-42e7-8382-0b0a368ae065           Christine Barton                        reedamanda@rice.com           Beauty         Season         1              312.62            312.62  Mobile Payment    2024-07-27        Georgia            63   Other
    194  fb570667-049e-498c-8eaa-9945b41bd720              Anita Robbins                   miguelnorris@pittman.com             Home             Mr         3               60.32            180.96      Debit Card    2025-03-25     California            43  Female
    195  01e2a742-3379-4b07-bc50-75a936e1e4b2             Melissa Howard                        william86@gmail.com             Toys        Another         5              276.82           1384.10     Credit Card    2024-06-26     California            42   Other
    196  1abe919a-4b01-4caf-81bf-e4807d12dc41            Mary Harris PhD                            vquinn@cook.com             Home           Cold         1              317.68            317.68            Cash    2024-09-08          Texas            40   Other
    197  57ba0d04-9eb7-4311-af75-115f513ffc8a               Meagan Mcgee                         john82@hotmail.com             Home          Heavy         3              204.17            612.51  Mobile Payment    2025-01-06       Illinois            24   Other
    198  e668dd4c-f4d5-4b5d-a143-29ab3cf404d5          Denise Strickland                          adiaz@hotmail.com       Automotive            Too         3              108.67            326.01     Credit Card    2025-04-15   Pennsylvania            44    Male
    199  b9498208-a0d3-4cee-94e7-c785d32c433c               Anthony Cole                  nkrueger@ashley-myers.com           Sports          Check         3              330.47            991.41          PayPal    2024-08-16           Ohio            52  Female
    200  968de7e7-0651-4e61-b8e5-76344ffc3307            Anthony Gardner                        agibson@russell.com             Home           Rest         1              360.31            360.31  Mobile Payment    2025-04-02       Illinois            51    Male
    201  31bcc2cf-0349-4005-b2f6-514705df2ba9           Matthew Anderson                   melissadouglas@gmail.com           Beauty           Door         4              187.18            748.72     Credit Card    2024-06-28     California            25   Other
    202  1f03fff2-6476-45d5-a419-7c85eafa86da                Ashley Hull                         chase30@barnes.com      Electronics          Stage         1              176.27            176.27          PayPal    2025-02-08       New York            63    Male
    203  dcb8807a-4c1a-4386-ba12-487f09dcde90               Sheila Eaton                     danielpowell@green.net           Sports           Sign         1              164.24            164.24            Cash    2024-07-12   Pennsylvania            35    Male
    204  659d2712-544e-4112-9862-2568e6f424c9            Austin Hatfield                   richardcoleman@gmail.com        Groceries        Century         1              247.62            247.62      Debit Card    2024-12-27       New York            68    Male
    205  2d8c936d-adcc-4458-9540-b80f2f53b461             Nicholas Combs                       tiffany21@powers.org        Groceries         Friend         5              153.13            765.65     Credit Card    2024-08-23           Ohio            36  Female
    206  3b6d7b29-0251-411c-9959-03256d5cfabb             Matthew Foster                aaron81@hamilton-decker.net             Home            How         1              103.38            103.38  Mobile Payment    2025-02-15     California            54  Female
    207  ad7e055a-16c4-4016-a954-fc2b613a1d2b              Ashley Medina                    sandersdaniel@yahoo.com             Home              A         3              321.78            965.34     Credit Card    2025-04-01       Illinois            45   Other
    208  eb11a4f8-4494-456d-9c5f-fd3e0117bf90               Ashley Clark                       ashleydiaz@moore.org             Home        Realize         1              190.95            190.95  Mobile Payment    2025-04-11        Florida            19    Male
    209  b1127e22-79f7-4ddd-a9f0-b0d5a8acd2ce              Gregory Cross                          lance90@meyer.com        Groceries          Month         5              483.01           2415.05     Credit Card    2025-04-17   Pennsylvania            36   Other
    210  0154c84f-bab1-4ecc-9f73-9104b8aa5873             Kenneth Parker              danielleprice@pineda-tran.com      Electronics          Plant         1              252.81            252.81      Debit Card    2024-08-01   Pennsylvania            25    Male
    211  2626ba75-2230-4f75-aff6-899376d087b3              Michael Kelly                    sarahalvarado@yahoo.com             Home            Not         3               37.92            113.76            Cash    2024-07-13        Florida            55   Other
    212  60300d7f-639b-4680-94b5-13ba49a33d32             James Thompson                   williamallen@hotmail.com           Beauty       Daughter         4              457.84           1831.36     Credit Card    2024-06-18   Pennsylvania            60  Female
    213  169ae64a-6870-4772-a479-80984e9c9284              Edward Arnold                          xmartin@yahoo.com         Clothing         Simple         4              481.37           1925.48  Mobile Payment    2025-01-03       New York            59    Male
    214  e7cadd47-465d-4d95-8150-a60430f564bf            Cynthia Dickson                         jhanna@hotmail.com       Automotive          Three         5              413.09           2065.45          PayPal    2024-10-29     California            58   Other
    215  3a1dedee-e770-4b8e-935e-063ec962c940              Julie Hopkins               sandra26@larson-callahan.com       Automotive           Poor         1              347.63            347.63          PayPal    2024-08-10   Pennsylvania            49    Male
    216  effd9716-9895-4967-be34-0fc54ff67d9c             Brian Mccarthy                    davisjennifer@yahoo.com      Electronics         Almost         5               53.02            265.10      Debit Card    2025-03-07          Texas            55  Female
    217  d90d067a-4bf5-45db-971b-2cbb372a785e            Jeremy Fisher V                        michael38@yahoo.com        Groceries           Pull         4              449.23           1796.92      Debit Card    2024-06-07          Texas            26    Male
    218  8a50442c-c3d4-4a07-8dcd-9ac1a82826fe       Timothy Mitchell III                    wilsoncynthia@gmail.com       Automotive          Mouth         5              146.59            732.95     Credit Card    2024-08-11       New York            18   Other
    219  098f23f5-86a6-44a5-8e7a-5d337e48d77d             Michael Howard                    gonzalezkaren@yahoo.com           Beauty           Save         5              463.82           2319.10          PayPal    2025-03-20       Illinois            20    Male
    220  6bd7a09a-f01a-4ebd-9c2b-46ed8fdffdc3               Robert Garza                   fergusonvalerie@rios.org           Sports          Stock         5              114.25            571.25          PayPal    2025-03-03       New York            48   Other
    221  0971670e-bc75-4b52-a1a8-47a927de4ea6             Zachary Harris                   morrismichelle@owens.com      Electronics          About         3              134.70            404.10     Credit Card    2025-04-30     California            29  Female
    222  dbb803c2-6a76-44e6-8799-b3c7a780961b                 Jody Jones                      ytrevino@thompson.com             Home           Plan         3               85.52            256.56  Mobile Payment    2025-01-04        Georgia            55    Male
    223  79505b73-cc3c-45ff-9e18-26a73423e2d0             Valerie Bailey                 jessicagarza@cervantes.com       Automotive         Window         2              100.77            201.54            Cash    2024-08-23          Texas            61  Female
    224  2e50f1fd-d8ff-4ad7-b6e9-91d35e64a1e9              Brenda Ashley                         idennis@willis.biz           Beauty           Fish         3               81.60            244.80          PayPal    2025-02-11     California            65   Other
    225  25cf10aa-3b5f-4658-8877-1add07669b63                Martin Bean                   kimberlybryant@gmail.com        Groceries            May         5              190.27            951.35          PayPal    2024-07-25        Florida            35  Female
    226  71e3f069-b86a-433d-8866-11d70e367f3b               Daniel Kelly                        dominic43@yahoo.com        Groceries         Window         2              249.41            498.82            Cash    2025-05-01       New York            21   Other
    227  e86c9e18-dc20-4093-ae21-c24dd2aac4f5          Jennifer White MD                          qwest@hotmail.com           Sports           Look         4              124.57            498.28     Credit Card    2024-07-15     California            52   Other
    228  87ad4ff1-3b5e-41e0-8669-c1c320091a54             Heather Parker                          sreeves@burns.com        Groceries         Strong         1              375.04            375.04          PayPal    2025-01-02        Georgia            45    Male
    229  9765236c-dd52-4f6f-8699-3d5c3e200bab               Joseph Roman                  carterlindsey@hotmail.com           Sports         Anyone         1              243.85            243.85  Mobile Payment    2024-07-06       New York            50   Other
    230  227cd45d-74c9-40dc-879c-80373822d4e5              Manuel Suarez                    davidreynolds@scott.com           Beauty         Leader         4              309.56           1238.24            Cash    2024-09-29     California            52    Male
    231  2bd8f8b3-9846-4483-b3da-fc314da6b596               Charles Barr                          yadams@adams.info             Home         Reveal         2               18.35             36.70     Credit Card    2024-10-21     California            60  Female
    232  5e9570d7-c6bc-42af-a3e9-3ea2a4b104c4              David Carlson                     flemingderek@gmail.com         Clothing           Move         5               61.21            306.05  Mobile Payment    2024-12-07       New York            68   Other
    233  8de5aea5-b2a6-4395-b987-fc91238e8312              Monique Olsen                        joshua06@landry.com             Home         Others         1               60.40             60.40     Credit Card    2024-05-03   Pennsylvania            30   Other
    234  7d9433a9-4def-42c1-a47d-6c0d874170aa              Scott Parrish                     billyscott@andrews.com           Beauty           Bill         4              140.66            562.64      Debit Card    2025-04-13           Ohio            63    Male
    235  ab9bb153-013c-4391-b4d4-194f0a1a1daa            Jessica Edwards                        douglas71@yahoo.com         Clothing            But         3               82.57            247.71            Cash    2024-06-14        Florida            59   Other
    236  658544ea-b8cf-44fd-8160-a29b7e7a66f3             Carlos Johnson                          megan50@gmail.com           Beauty           Deal         2              161.67            323.34          PayPal    2024-10-05          Texas            67  Female
    237  6578ecbd-ebf6-48a2-9188-ff8338d78c1b             Thomas Frazier                  cameronjeremy@bridges.com         Clothing        Defense         2              217.04            434.08     Credit Card    2025-03-11          Texas            28  Female
    238  80787ee1-3700-4a53-ac52-f7173055bea6              Tammy Ramirez                joseph37@ortega-marquez.com        Groceries      Political         5              348.56           1742.80          PayPal    2024-12-10       New York            69  Female
    239  d9f62caa-5cb1-4ba5-8142-ec7291138ec2               Barbara Todd                michaelanderson@hotmail.com      Electronics        Teacher         3              446.37           1339.11      Debit Card    2025-03-13           Ohio            31  Female
    240  7cf6188c-2794-42f1-93c3-764f35d501d8               Barbara Webb      heatherrandolph@marquez-hendricks.net           Sports           Keep         4               55.01            220.04            Cash    2024-09-02           Ohio            66   Other
    241  020b8220-d25e-48db-9ba1-0832aa47110d               Amanda Jones                         joseph78@gmail.com           Sports     Management         1              404.86            404.86          PayPal    2025-04-01       Illinois            42    Male
    242  ebb1065c-4858-4dc6-8560-b3f6bbda225f              Jamie Sanchez                         sknight@meyer.info           Beauty         Within         4               33.28            133.12            Cash    2025-01-05           Ohio            70   Other
    243  50001c85-c4a3-40fd-b3b7-4c44b11f02bd              Matthew Jones                  johnsonelijah@hotmail.com        Groceries        Pattern         1              121.60            121.60  Mobile Payment    2024-06-16     California            59  Female
    244  c6452123-6afe-4f66-85e1-1e8ad226ac9e              David Lindsey                            breed@yahoo.com        Groceries            Its         1              458.79            458.79          PayPal    2024-07-19       New York            69    Male
    245  65c4f8e2-95fd-4057-b6e2-97f7ddbea1c8            Mitchell Torres              cobbjill@macdonald-wilson.biz      Electronics           Half         5              456.86           2284.30          PayPal    2024-05-07           Ohio            63   Other
    246  2e604258-18cf-4bc1-b94d-50c38962852e             Charles Morris                    sabrinaryan@jackson.com      Electronics       Question         4              131.36            525.44            Cash    2024-07-30       Illinois            70   Other
    247  d3786573-c860-4241-9268-37744503e714                Sara Nelson                      sandersalan@gmail.com      Electronics      Agreement         2               27.01             54.02            Cash    2024-05-19     California            26  Female
    248  127f07f4-ecaa-470d-b871-cfdfc356d6c1           Jeremiah Collins                          dwillis@brown.com           Beauty        Society         5              352.75           1763.75      Debit Card    2025-02-12        Florida            25  Female
    249  69249d8c-f21e-420c-a12f-e117b2c0e918                Paul Nelson                           krowe@fields.com       Automotive          Sense         3               98.66            295.98     Credit Card    2025-03-23   Pennsylvania            62    Male
    250  bb21f2f3-56e4-49a9-b6f5-9772fa61ed2b                 Aimee Lara               chelseyanderson@gonzalez.org        Groceries        Central         4               80.54            322.16  Mobile Payment    2024-08-10          Texas            47    Male
    251  f4c6dbec-9283-4377-bfbd-8d98c843da06            Nicholas Martin                       zhowe@richardson.com      Electronics       Election         3              222.21            666.63     Credit Card    2024-07-13           Ohio            65    Male
    252  ffe7e7df-d093-438f-82b4-1fa8dc0d0f90            Aaron Rodriguez                 jennifercastillo@yahoo.com             Home           Hour         1               38.08             38.08            Cash    2025-02-14       New York            50   Other
    253  490543a2-d40f-4780-b75e-2efa69a9c156             Anthony Campos                        ythornton@gmail.com      Electronics           List         4              495.82           1983.28  Mobile Payment    2025-04-15   Pennsylvania            70    Male
    254  ab3b40bb-a7cb-4829-b570-2971b9162135               Monica Berry                     michael22@mckenzie.com           Beauty         Moment         5              219.75           1098.75  Mobile Payment    2024-10-03     California            43    Male
    255  71edb012-d95a-40ab-9ad0-d4cc582bcebc                 Ross Davis                      michaelwebb@yahoo.com      Electronics       Marriage         2              189.21            378.42          PayPal    2025-01-28     California            23   Other
    256  453b794e-38cf-48cf-a5b9-713157ed1ec2            Elizabeth Brown                          twalton@gmail.com           Sports         School         5              441.03           2205.15          PayPal    2025-01-31     California            41    Male
    257  1d2a5a1f-e7d1-401b-a328-dbe3dd15ec4d              Crystal Jones                   jenniferadkins@gmail.com       Automotive          Serve         5              128.50            642.50  Mobile Payment    2024-08-08     California            33  Female
    258  a1529616-97a1-4b0b-8260-b7643bd14591               James Jordan                        craigtony@jones.com      Electronics          Prove         2              433.55            867.10     Credit Card    2025-04-29       New York            54   Other
    259  e6a36137-4503-4a74-b8c8-bdce9782a9ea               Laura Becker                           pallen@silva.com       Automotive          Focus         3              441.74           1325.22      Debit Card    2024-07-01        Georgia            24   Other
    260  5ea3095c-736b-49b9-9593-726a25e1c415            Travis Williams                     chenashley@hotmail.com           Beauty         Around         3              382.79           1148.37     Credit Card    2025-03-15       Illinois            69  Female
    261  7b2385bb-d1b1-4749-a2a9-85017ac4c963                  Anne Hall             colleen62@pearson-stephens.com             Toys          Admit         3              485.05           1455.15      Debit Card    2024-10-12           Ohio            41   Other
    262  c16ceb1a-6b55-42db-818c-15fcec29759c                David Kelly                          zgeorge@yahoo.com        Groceries          Begin         5              181.59            907.95     Credit Card    2024-12-17       Illinois            68   Other
    263  b0bc2abc-7209-43b2-b7c1-93c03745fde9                Hunter Ford                          lisa17@taylor.com       Automotive           Star         1              271.53            271.53      Debit Card    2024-09-20        Florida            40    Male
    264  634e1b71-cae7-4354-9ca6-8f3f6869a7de                 Tony Smith                         bjohnson@yahoo.com           Sports            End         4              429.57           1718.28  Mobile Payment    2024-06-09        Florida            44  Female
    265  5b16283a-813d-434f-807f-78b2c496fa9f           Kristin Campbell                      xsantiago@hotmail.com        Groceries             My         3              130.24            390.72     Credit Card    2025-02-03   Pennsylvania            35   Other
    266  a3e706f6-0d5e-4295-8634-8c0e68154058         Catherine Hamilton                       ihernandez@henry.net       Automotive          Argue         3               60.65            181.95  Mobile Payment    2024-10-21       New York            22    Male
    267  6a9f5865-ef33-43a5-9f3a-2ab08c4e3536                 Tammy Hill                          ralph00@terry.net       Automotive        Respond         4              307.54           1230.16          PayPal    2025-04-01           Ohio            41    Male
    268  a3872dbc-6138-4159-bed5-cf348c4dfa31             Benjamin Davis                      allison45@hotmail.com         Clothing         Sister         1              353.68            353.68  Mobile Payment    2024-09-29          Texas            35  Female
    269  b55b634c-a8d5-4a83-b43c-9d3a49b36f52                Marcia Hunt                         autumn09@brown.com           Sports        General         4              104.02            416.08          PayPal    2025-02-08          Texas            33   Other
    270  820af631-bf43-4230-acb1-928cfe164596              Sheena Cherry                          unewman@gmail.com         Clothing            Ask         4               56.49            225.96  Mobile Payment    2024-06-21           Ohio            51    Male
    271  6ee897c2-a993-4935-b7d9-de127244d354               David Benson                    tony28@lowe-gilbert.net             Toys        Respond         4              360.75           1443.00            Cash    2024-07-29        Florida            29   Other
    272  474a962d-8aff-4334-906b-c95ecf0bdcf4          Michael Alexander                   jonathanthomas@gmail.com      Electronics           Thus         3              340.27           1020.81      Debit Card    2025-04-30       New York            62  Female
    273  f7944cf9-f460-47c6-8812-87cb0ab8bac3             Julie Humphrey                        tanya57@hotmail.com         Clothing          Great         1               78.28             78.28            Cash    2024-07-16     California            53   Other
    274  75927c63-3aa6-4a12-ba3b-cd411d198442              Andrea Taylor                         autumn85@lopez.com        Groceries          Young         1              225.66            225.66          PayPal    2025-04-09       Illinois            49  Female
    275  e8277751-e875-4c99-8577-7d62d778b558           Danielle Vasquez                         oparsons@yahoo.com         Clothing          Eight         3              183.83            551.49      Debit Card    2025-02-01   Pennsylvania            25  Female
    276  35b2632c-bebf-4d52-b606-c7b1776236b5            Ashley Stephens                    youngemily@anderson.net      Electronics          Large         3              425.17           1275.51      Debit Card    2024-08-03       Illinois            50  Female
    277  761736d5-0c4b-4f8f-888a-6065d296b0a4           Morgan Hernandez                           adam25@allen.com             Toys         Behind         2              215.07            430.14          PayPal    2025-03-06   Pennsylvania            41    Male
    278  b5a45dd5-1c60-4986-972b-a36d60f296d4             Stephen Curtis                    toddmartinez@bailey.org             Home           Step         3              462.45           1387.35      Debit Card    2024-09-15        Georgia            51  Female
    279  e05668a5-df76-4a84-9107-1c427b1db5ce            Kimberly Walton                        uthompson@gmail.com           Sports     Individual         4              152.65            610.60      Debit Card    2025-04-07        Georgia            18    Male
    280  6508854a-6153-43ee-88b0-aa470220d4f1             Belinda Taylor                 kelli89@simmons-wilson.net         Clothing          Drive         3              431.48           1294.44            Cash    2025-01-30           Ohio            39  Female
    281  cf09fad0-3e0d-4ed2-9473-74a590f080f9               Brian Jordan                    barrylewis@morrison.com      Electronics          Admit         3              148.63            445.89      Debit Card    2024-12-13     California            51  Female
    282  4b4acb93-3caf-49b6-bad6-852d3c2c10e9              Rachel Tanner          vazquezmary@pollard-hernandez.org       Automotive        History         1               19.77             19.77          PayPal    2024-12-05          Texas            29   Other
    283  09cce515-704d-4771-9e16-e53a906d9c4d                Laura Banks                       fhernandez@lyons.com           Beauty            Pay         1              310.55            310.55     Credit Card    2024-06-01           Ohio            37   Other
    284  7dd84fd0-3d5c-4093-87cc-5f4420f161e0              Jenna Johnson                       tspencer@hotmail.com           Sports       Decision         1               61.67             61.67            Cash    2024-07-03          Texas            66  Female
    285  dcf91e1c-30ee-4e7d-a588-d8f9725b8271               Karen Thomas                        timothy55@yahoo.com      Electronics           Send         1              102.46            102.46      Debit Card    2025-04-21       New York            21  Female
    286  a42f8bf8-2069-457d-9c3c-2043a92042fd                 Paul Allen                         ogriffin@davis.com      Electronics         Policy         5              211.58           1057.90          PayPal    2024-11-02        Georgia            20  Female
    287  02f5eae2-b912-4e65-a251-a412660717e7              John Ward DDS                   justinnorton@hotmail.com       Automotive          Still         3              434.81           1304.43          PayPal    2024-11-05          Texas            41   Other
    288  10e4735d-998e-460d-bcba-901e5a1fe635                 John Klein                     arroyoeric@elliott.com             Toys           From         4              120.90            483.60          PayPal    2024-07-25       Illinois            65    Male
    289  827e1641-3e29-4b62-897e-0f97fa4bac2f         Andrew Johnson DDS                  dianaharrington@yahoo.com             Home             Pm         3               14.98             44.94  Mobile Payment    2024-09-26          Texas            63   Other
    290  8b6ac0bd-ee9c-493b-8ec9-de3c41fa4aa7              Jessica Smith                      barbara46@hotmail.com             Home         During         3              193.28            579.84  Mobile Payment    2024-05-16        Florida            20  Female
    291  04217909-c157-4d16-a21c-3465f79fad70               Lisa Goodwin                         fbennett@yahoo.com             Toys         Theory         1              318.25            318.25  Mobile Payment    2025-01-26       Illinois            48   Other
    292  6b065988-ec85-4dbd-9605-4ecc2fe1dadb               Zachary Ford                      johnramos@hotmail.com       Automotive        Thought         4              298.45           1193.80            Cash    2024-07-21     California            35   Other
    293  ae79d91a-4971-48a1-8973-e627f8da2334              Shirley Ramos                kmiller@kramer-hamilton.com           Sports     Population         4               54.24            216.96  Mobile Payment    2024-07-17       New York            45   Other
    294  893a0976-5b38-44fb-8c9c-bd33af03b097                Mathew Horn                           yramos@gmail.com         Clothing           Lose         3              156.37            469.11      Debit Card    2024-10-11       Illinois            31    Male
    295  3a64765f-ca3d-40d1-85e5-2b4135029695                 Dana Gomez                   swansonscott@cameron.com           Sports            Sea         3              176.61            529.83          PayPal    2024-05-17   Pennsylvania            55    Male
    296  9f3f70df-7f77-4d88-a738-77b4ca66d630               David Wright                        charles97@yahoo.com         Clothing         Become         4               59.89            239.56     Credit Card    2025-01-17        Georgia            36   Other
    297  bfeec3f2-2ce1-437e-abb7-47fe1d79d572             Clayton Hughes                         dawnmann@gmail.com         Clothing          Fight         3              270.50            811.50      Debit Card    2025-01-18        Florida            68  Female
    298  e579dc6e-50c3-43bc-b361-6bb107bad7a4        Angela Mckinney DDS                          jake80@howard.org      Electronics           Know         3              198.59            595.77  Mobile Payment    2025-04-15       Illinois            20    Male
    299  4dc6d651-a5ef-4d99-a9ca-ee465d1445f0           Christine Harvey                           gayers@gmail.com           Beauty          Early         4              491.54           1966.16     Credit Card    2025-04-12       New York            30    Male
    300  f49c7225-9268-414a-9242-37ea0926b22a          Elizabeth Collins                           ygross@yahoo.com             Home           They         1                8.12              8.12            Cash    2025-01-18   Pennsylvania            55    Male
    301  94b6c21b-0071-4be0-833a-36d82461914e              William Gomez                          james29@davis.biz           Sports            Yes         4              269.51           1078.04            Cash    2025-01-02          Texas            46   Other
    302  59d7e556-7605-4d50-b6b3-3d2ef539fbf9               Kenneth Gray              ruthtucker@bruce-johnson.info      Electronics       Specific         2              321.35            642.70  Mobile Payment    2024-05-04     California            60  Female
    303  4bc4a40a-f50c-4ae8-a335-1bfc2cb06fbf                Wyatt Silva                            ydavis@west.com             Home           Wish         4              498.04           1992.16            Cash    2025-05-02     California            67  Female
    304  5c5ff1df-f79e-41a7-a034-f84db7f0d3b8             Cynthia Hughes                 morrissamantha@hotmail.com           Beauty         Assume         3              126.19            378.57  Mobile Payment    2025-04-11       Illinois            28    Male
    305  4f099145-76e8-4cad-9572-2bfd457e87fd             Kevin Fletcher                       fisherpaul@hurst.com             Toys             In         5              354.56           1772.80          PayPal    2025-02-18     California            22   Other
    306  7c654eb0-1c7d-4b02-96c8-44db05f45201                Travis Odom                        ychurch@daniels.com       Automotive          Crime         2              246.83            493.66            Cash    2024-08-22        Georgia            23  Female
    307  aae5d89f-ad21-4b4b-b7a2-f36949f89533           Alexander Suarez                     robertnewman@cross.com        Groceries           Five         4              477.32           1909.28      Debit Card    2024-10-15     California            40  Female
    308  89f3f485-9921-4289-b618-5a68500654d3          Theresa Rodriguez                       wlarson@shepherd.org         Clothing       Election         4              261.27           1045.08     Credit Card    2024-07-19     California            32    Male
    309  87b7f2b0-7aaa-4945-97c3-6e9c466e7cf0                 Mary Evans                         cmoore@hotmail.com      Electronics           Face         1              392.52            392.52          PayPal    2024-11-01   Pennsylvania            54   Other
    310  9af030d9-e7e2-4901-a622-6e885cc99443           Antonio Castillo                     mooredavid@hotmail.com         Clothing         Writer         4              298.06           1192.24            Cash    2024-08-27           Ohio            27    Male
    311  e5822e32-0f15-4826-aa61-76cc1d2401e3             Theresa Wright                     cameronprice@gmail.com         Clothing         Across         4               53.02            212.08     Credit Card    2024-10-02       New York            54  Female
    312  55c66c2c-1a6a-46e1-b216-cc928b142064                Gavin Moore                        phillip19@gmail.com           Beauty         Church         2              383.40            766.80      Debit Card    2024-06-26        Florida            64  Female
    313  9ef136d6-9333-4a62-9f02-682c85b06ad2          Jennifer Woodward                        robin63@aguilar.com         Clothing        Respond         1              285.24            285.24     Credit Card    2025-01-26          Texas            22   Other
    314  6c06a410-5355-44cf-96b3-150d06b8d2f5             Anthony Hebert               davissteve@freeman-silva.com         Clothing         Arrive         4              207.37            829.48            Cash    2024-05-20        Florida            51   Other
    315  38a30dea-a783-4f87-9647-30944a7db7db                 Tina Mason                          nlozano@davis.com             Home          Ready         3               26.46             79.38  Mobile Payment    2025-03-01   Pennsylvania            54    Male
    316  8d5bc75a-ff80-4b85-9d6b-1e6bb4ebc125            Alexander Wolfe                    christopher93@yahoo.com        Groceries           Vote         1              315.70            315.70          PayPal    2024-11-24           Ohio            36    Male
    317  85e0d49c-29d0-44a6-8e2d-4d657117edc5              Sally Bradley                      boyerjessica@west.com             Home            Few         5               57.76            288.80     Credit Card    2024-12-21          Texas            48  Female
    318  92d10cbf-9c67-4b10-bf99-e919b1c5b199             Michelle Meyer                         jamescox@yahoo.com        Groceries          Piece         2              163.26            326.52     Credit Card    2025-01-15        Georgia            65   Other
    319  1028f19d-cf5f-4395-abdb-6dfcd1809c54           Gregory Martinez                           john12@yahoo.com      Electronics        Western         2               87.59            175.18            Cash    2025-04-05   Pennsylvania            63    Male
    320  486b110c-7b0e-4c6c-9036-5203a75aeb4d             Sharon Andrade               christophershort@hotmail.com        Groceries           Road         3              424.29           1272.87            Cash    2024-07-14           Ohio            32   Other
    321  20245fa9-eec8-468b-8486-40697fc70b6c            Robert Martinez                      johnpotts@hotmail.com             Toys          Radio         2              491.49            982.98      Debit Card    2025-01-02   Pennsylvania            39  Female
    322  764f8008-cede-4ca4-85aa-06dbeb56f434          Jessica Allen PhD                      heatherlamb@yahoo.com           Sports         Behind         5               64.69            323.45     Credit Card    2025-01-13     California            52   Other
    323  90dcc76c-52aa-48c8-b5f2-01f86f6c04b1              Tyler Rodgers                           troy80@yahoo.com           Beauty         Health         2              197.97            395.94          PayPal    2025-02-11        Florida            69   Other
    324  5c3e399c-ecc2-4e44-881b-cf7719629a31                Perry Young                    eharrison@bray-chan.net       Automotive       Magazine         1              467.54            467.54          PayPal    2024-05-24          Texas            52    Male
    325  3e708052-a73a-4077-8c88-fc08f81ea316                Jesse Frost                          hunter27@shaw.com             Toys           Past         4                6.02             24.08     Credit Card    2024-08-15           Ohio            53   Other
    326  c7b35c62-dc99-47cb-a97a-434b14dfa461               Ricky Thomas                          maria88@yahoo.com           Sports           Seem         1              395.97            395.97            Cash    2024-11-07       Illinois            36   Other
    327  8c9c6d4a-5685-4a6c-ac19-9ac2ab6f9d65            Lindsey Johnson                        timothy20@yahoo.com             Toys           Fact         1               20.44             20.44            Cash    2024-09-01           Ohio            41   Other
    328  920d5883-5141-4677-9b36-60b665571d67                Lisa Murphy                         curtis51@gates.com             Home       Interest         2              226.48            452.96            Cash    2024-08-14     California            47   Other
    329  25031303-edeb-426d-9ecc-8284f40d5f66                 David Cobb                     jimmynavarro@gmail.com           Beauty         Weight         1              281.73            281.73          PayPal    2024-09-15           Ohio            20   Other
    330  229f575d-b9bf-4d78-b838-8f00a4d271af           Joseph Stevenson                 lauren98@fowler-fowler.com             Home           Grow         2              118.56            237.12          PayPal    2024-11-20        Florida            63    Male
    331  3f9c36f4-8901-4d9c-9b1d-ef5ab18e4c20           Chelsea Mckinney                      matthew53@hotmail.com        Groceries       Standard         4               54.42            217.68            Cash    2025-03-21        Florida            69   Other
    332  d68a846b-7ec2-48ee-84a9-ff0e1b68896e                Ronnie Haas                    stevenwoods@hotmail.com       Automotive            One         1               41.06             41.06     Credit Card    2024-09-09          Texas            19  Female
    333  ec0e069b-db67-41a8-94b7-010393cc98c3                 Jason Cook                  melissareynolds@yahoo.com       Automotive           Face         3              104.44            313.32  Mobile Payment    2024-10-17        Georgia            68   Other
    334  53be0ce4-9a0f-459e-bc23-3aa86545f085             Patricia Cohen                         krista96@gmail.com             Toys          Story         5               84.84            424.20  Mobile Payment    2025-02-16           Ohio            25  Female
    335  7390058f-9566-4326-b9df-c0dc7c78002b              Dylan Cochran                    robertsjames@wright.net           Sports          Carry         2              182.84            365.68            Cash    2024-09-27     California            33  Female
    336  1979d2ea-7477-4111-ab81-7484f085186e                 Alan Jones                     blackderrick@gmail.com             Home           Bank         2              285.30            570.60            Cash    2025-01-18        Florida            40    Male
    337  7303d874-a216-4d69-bc96-36f4159dba07               Elijah Moore                         zstark@hotmail.com             Toys           Step         2              479.64            959.28      Debit Card    2025-01-25       Illinois            49    Male
    338  8aa77a42-41ac-44f9-b9de-e8473803af21              Vincent Myers                       amendoza@hotmail.com           Beauty         Letter         1              158.19            158.19            Cash    2024-12-23       New York            58   Other
    339  98b53d83-2c32-4ffa-9f3a-c9b29f0f6721          Margaret Griffith                  zcruz@phillips-monroe.com           Beauty           Even         3              140.51            421.53      Debit Card    2025-01-30       Illinois            30   Other
    340  4d9d4d5c-5608-41ab-ad90-d9e7d31ed71c              Stacey Garcia                          amber80@yahoo.com             Toys          Eight         2              276.82            553.64            Cash    2024-06-06     California            68  Female
    341  e50c255b-82b0-490e-9101-fce69165edd6               Larry Walker                     mckenzie73@collins.com           Sports         School         5              366.75           1833.75      Debit Card    2024-10-06     California            65   Other
    342  1edc1e8b-bbd6-421f-9928-49be51bed5c5                Susan Owens                            mking@marks.com           Beauty            Way         3              332.35            997.05      Debit Card    2024-11-06     California            44   Other
    343  68769a50-4cbe-477d-8745-a4a60f653ff0           Pamela Rodriguez                          imiller@gmail.com           Sports        Feeling         5              135.00            675.00      Debit Card    2025-04-10     California            52  Female
    344  f08e105b-6fe4-49f3-a7a4-504d5853c483              Robert Wagner                jessicamathis@martinez.info       Automotive           Meet         4               10.85             43.40          PayPal    2025-04-23     California            20    Male
    345  bb22573b-5d24-4fc3-af1c-bd8bd30e9d13                Kayla Jones                  danielleswanson@gmail.com        Groceries        Usually         5               92.80            464.00  Mobile Payment    2024-07-03           Ohio            18   Other
    346  29cde9cf-33b2-451a-98e6-3a9e77a49269             Jennifer Lewis                 carolynstephens@wright.com           Sports          Final         1              335.21            335.21            Cash    2024-10-07   Pennsylvania            18    Male
    347  f873097c-6e96-438c-a9cc-80757c2033e3            Matthew Shannon               donnadominguez@king-cruz.com        Groceries       Computer         2               32.51             65.02            Cash    2024-05-15        Florida            37   Other
    348  ade00831-1826-404a-a973-edb473bd0dd5             Jeremiah Owens                    howardkirby@hotmail.com        Groceries        Involve         3              350.40           1051.20     Credit Card    2024-08-18     California            67    Male
    349  03bb3c36-c10c-473e-a71a-1ab30f3e3df7             Jeffrey Sawyer                       teresa81@stewart.com             Toys           Grow         3               20.55             61.65     Credit Card    2024-08-23       New York            48   Other
    350  58013952-67b3-4ef8-b873-3d3dcc726e99              Donald Miller                     smithjames@perkins.org           Sports     Collection         5              221.48           1107.40     Credit Card    2024-09-27        Florida            28    Male
    351  81b56e33-0ab0-43c0-9f3f-1f1fa683afaa            Kristin Aguilar                       dwayne00@collins.com           Beauty          Space         5              187.00            935.00      Debit Card    2025-04-09   Pennsylvania            26  Female
    352  1afdd27d-e811-4151-b7f6-6954afe3e277         Matthew Fitzgerald                      paynesamuel@gmail.com             Toys           Into         2              250.94            501.88  Mobile Payment    2024-11-01     California            50    Male
    353  d6ae4f3a-aa10-4961-8e36-3bcfc86f04e9               Morgan Heath                    hallalexander@gmail.com       Automotive           Late         5              410.60           2053.00  Mobile Payment    2025-05-02       New York            23   Other
    354  8b5192a5-589f-4dc5-b214-7abece6d5ffc             Joseph Jenkins                  sheilakramer@sanders.info       Automotive          Blood         5               61.39            306.95            Cash    2024-05-16       Illinois            49   Other
    355  bcd651fc-69b3-4df1-9d46-9e30cf97b0d2                 Erin Bruce                 erica82@powell-freeman.com      Electronics             So         5              274.94           1374.70     Credit Card    2024-12-19        Georgia            70   Other
    356  b0a9e9ef-59b9-436c-8de8-d522442cbd30                 John Dixon                          nmartin@woods.com             Toys             At         4               48.30            193.20      Debit Card    2024-09-24          Texas            47    Male
    357  02bfdfcb-2c48-4b40-b306-41f3a448a55c               Ryan Garrett                           zmoore@gmail.com           Beauty           Stop         1              313.12            313.12          PayPal    2025-03-14        Georgia            63    Male
    358  ab8c9be7-7a5e-4c71-9d57-0f841b4ee2c4            Yolanda Nielsen                     lindseyjulie@gmail.com           Beauty           Half         3              216.68            650.04  Mobile Payment    2025-05-01     California            60    Male
    359  e5c50e58-15a6-48e0-b607-e059aa4e35ac             William Lozano                       scott46@bautista.com        Groceries           Move         2              465.05            930.10          PayPal    2024-06-02           Ohio            29  Female
    360  cbde5e29-791d-4ac6-8693-cc4f4b1f8107            Taylor Guerrero            josephrogers@griffin-jordan.com       Automotive       Describe         1              224.56            224.56          PayPal    2024-09-10       Illinois            45   Other
    361  c7d9aea2-7165-425f-ba8d-08ff4e7435fb              Michael Logan                    grahamdiana@hotmail.com             Toys            Pay         5              245.96           1229.80            Cash    2024-08-19   Pennsylvania            31    Male
    362  6367e51e-63db-4c08-82e8-9169458ae9ba                  Noah Good               ahenderson@pope-griffith.com      Electronics           Ball         3              343.65           1030.95      Debit Card    2025-05-02        Georgia            65   Other
    363  076bd974-4ed6-4117-8ce9-f97d1888dcbd              Justin Duncan                   taylormichelle@gmail.com      Electronics           Find         1              246.11            246.11     Credit Card    2024-11-03   Pennsylvania            67  Female
    364  78d4ee9c-a3d5-4d84-876b-23fd44b0ffb0              Edward Carson                 smithjennifer@griffith.com           Sports         Appear         5              345.90           1729.50            Cash    2024-06-28   Pennsylvania            41   Other
    365  f7208a86-89a3-4422-9852-f3052eea0940              Brian Spencer               savannahroberson@patton.info           Sports          Media         5              199.74            998.70     Credit Card    2024-07-06     California            34   Other
    366  ce4d0968-8063-43c8-b5c2-32af59e6a279                Mark Garcia                      drewclark@hotmail.com      Electronics          Group         2              300.86            601.72  Mobile Payment    2024-12-30        Georgia            60    Male
    367  e1a428a7-81e9-47a8-99ee-b13e5dafed95          Shannon Henderson                    stephanie43@wilson.info         Clothing            End         1              335.21            335.21  Mobile Payment    2024-05-08          Texas            36   Other
    368  f7bdc256-c151-4436-8784-19f81756ef0a              Kristy Holmes                       allengarza@rios.info         Clothing          Thing         5              490.24           2451.20     Credit Card    2024-12-06          Texas            49  Female
    369  7b3714fb-4595-4587-8c21-9c44fdeebf66             Zachary Powell                   jeremygraham@hotmail.com             Toys      Attention         3              383.89           1151.67          PayPal    2024-11-28   Pennsylvania            65    Male
    370  8ab7c87a-0916-497c-b24f-e4bc9919e3cb             Timothy Forbes                 ubradford@hill-webster.com             Toys         Leader         3              386.63           1159.89            Cash    2025-02-22     California            21    Male
    371  11937b19-3fbf-4c43-841e-91fd6923e694             Jessica Murphy                         bushlisa@gmail.com      Electronics        Million         1              212.62            212.62     Credit Card    2025-01-24        Florida            60  Female
    372  3b44684d-0a57-4f63-a724-05c609550774              Thomas Nguyen                     brianzamora@wilson.com           Sports          Third         2              302.51            605.02     Credit Card    2024-07-30       Illinois            28   Other
    373  3e3cc575-175e-40ce-839c-abd8f471ddd3              Emily Leonard                          aharris@yahoo.com       Automotive        Present         3              283.60            850.80     Credit Card    2024-07-05       New York            34  Female
    374  96bac5f1-d9ec-4cc3-b2f3-3ede5e0a0c7c            Ashley Odonnell                     pconner@wilkinson.info           Sports             Tv         3              466.96           1400.88          PayPal    2024-06-08           Ohio            30    Male
    375  92d86e98-5574-4d54-abad-5564e217c86c             Nicole Higgins                       ericadixon@gmail.com           Sports          Shake         3                5.09             15.27      Debit Card    2024-11-27           Ohio            68  Female
    376  5d31823f-4eaf-4782-a49e-24f8c1379e74             William Fuller            bentleysusan@sanchez-stein.info        Groceries           Sort         4              271.03           1084.12            Cash    2025-02-03        Georgia            20   Other
    377  a0d6eadc-1410-4572-a57d-9817ff0fe3a5             Lindsay George                   gcollins@rivera-paul.net      Electronics          Night         3               10.26             30.78          PayPal    2024-09-12     California            47   Other
    378  d3c979ff-a6f9-4d88-a08a-4baf7be56ba8           William Williams                         robert34@gmail.com       Automotive           Rock         2              405.90            811.80          PayPal    2024-08-04   Pennsylvania            65  Female
    379  adeda660-6ca6-4de1-917b-317cbe21ada0                Sonya Kelly                         sheila19@gmail.com           Sports        Defense         5               59.74            298.70          PayPal    2025-03-16       New York            69  Female
    380  a3900019-bd49-4c34-91e0-6327a0230fb1               Ivan Collins          michelebowman@franklin-greene.com             Toys          Final         4              254.68           1018.72  Mobile Payment    2024-05-13        Georgia            25   Other
    381  b5e2a3b2-a177-4e62-ae9e-1b54f00da85b           Jennifer Nielsen                 gloria86@soto-woodward.net      Electronics         Memory         1               45.40             45.40            Cash    2024-10-16   Pennsylvania            65    Male
    382  10f03dcc-f3b8-4421-a05b-fbb544428e5d                John Sawyer                 haydendavenport@garner.com        Groceries         Others         2              473.78            947.56            Cash    2024-07-22        Georgia            55  Female
    383  312e275e-6cf5-4472-99f5-519d8fe61207                Amber Ortiz                  timothy95@kelly-bowen.biz       Automotive          Fight         4              249.56            998.24  Mobile Payment    2024-05-15           Ohio            18   Other
    384  8280db0a-2883-4289-937a-8401ea097f2a            Jennifer Hester             leemartha@phillips-beltran.net           Beauty          Civil         2              146.21            292.42      Debit Card    2025-03-19   Pennsylvania            46  Female
    385  5a18d59c-e20d-4fd0-9d81-b8d3c80cd685            Ricardo Schultz                   bburton@hood-terrell.com         Clothing        Through         2               19.86             39.72          PayPal    2025-04-26   Pennsylvania            21   Other
    386  16cc1397-d2e8-4551-9b7b-adf7b88162b6            Holly Flores MD                     cummingsjames@beck.biz             Home          Above         5              237.48           1187.40          PayPal    2024-06-20        Florida            30    Male
    387  11e48ace-775a-4a4e-b260-8a46e5933c80                Susan Short                      cameron35@hotmail.com             Toys      Executive         2               75.29            150.58      Debit Card    2025-01-10          Texas            63    Male
    388  ceb670e8-658a-4f48-976f-1387417a9ba6                 Mark Ortiz                thompsonwilliam@hotmail.com       Automotive           Less         3              291.71            875.13     Credit Card    2024-11-22     California            31   Other
    389  85a7bc2d-45f8-4610-a2b1-58254b79e4cb           Allison Williams                       xmiller@sanders.info             Home          Party         1              280.15            280.15            Cash    2025-02-07   Pennsylvania            45  Female
    390  bc54551e-87f7-4b03-8f5c-98fbff4220be             Joseph Hancock                          fnelson@mejia.com             Home           Area         1              485.04            485.04          PayPal    2024-11-29       New York            60  Female
    391  1b59895c-096b-4f82-9273-fea78292f6f0        Bradley Christensen                          dpark@hartman.org         Clothing            Ask         4              206.36            825.44          PayPal    2025-04-06       Illinois            31  Female
    392  449828b7-18bf-4408-be45-f040e9b0782f            Johnny Cisneros                   robertthomas@hickman.com             Home          Local         3              242.30            726.90     Credit Card    2024-10-18          Texas            53  Female
    393  f86481a9-230a-4b0e-9f71-cf3f7ac8b02f              David Johnson                        jerry29@hotmail.com        Groceries           Hard         4               99.12            396.48          PayPal    2024-11-13       Illinois            26   Other
    394  2d595eb4-6b40-4cdb-8bf2-9019b5ca972b             Melanie Murray                          james80@yahoo.com             Home           Wear         5              385.89           1929.45          PayPal    2025-03-21       Illinois            66   Other
    395  82c6ef45-eebb-4bee-8f61-cc07d4859580                Joshua Hill                          laura24@yahoo.com             Toys         Really         3              438.32           1314.96      Debit Card    2024-09-15       New York            48  Female
    396  d51dfb1b-39f5-4f02-a740-38e5d9b1a1c6            Virginia Powers                    tcantrell@williams.info       Automotive    Information         1              253.89            253.89     Credit Card    2024-10-30           Ohio            69   Other
    397  482ad591-a6df-4b14-a28c-03ac36367ce3                 Daniel Cox               rebecca38@ramirez-harvey.com      Electronics        Perhaps         2               45.50             91.00            Cash    2024-10-21     California            40   Other
    398  5ecf7de4-cfea-4dba-a30d-ffc05ee8bfcb              Jeanette Gray                        scottsusan@owen.net             Toys        Special         3               92.16            276.48      Debit Card    2024-06-08          Texas            50   Other
    399  e6816c42-5d60-4e2f-a122-d908e843f5f0            Stacie Alvarado                 reynoldsrobert@hotmail.com         Clothing           Draw         4              404.19           1616.76            Cash    2024-07-28          Texas            26  Female
    400  e545a955-c828-469e-b1c2-43c798548552            Carolyn Spencer                          mwillis@gmail.com             Home  International         3              407.64           1222.92          PayPal    2025-03-10       New York            65    Male
    401  ddc545d3-47a7-4cd1-aba5-b73e76b1e5a6            Kenneth Raymond                      alidustin@vincent.com      Electronics          Voice         2               76.65            153.30  Mobile Payment    2024-05-30       Illinois            36    Male
    402  819041ce-eba7-42b3-890a-e5f8130bec8f               Angel Howard                           paul89@gmail.com        Groceries            Now         2              487.48            974.96     Credit Card    2024-08-24   Pennsylvania            32   Other
    403  e8a1b580-89d7-4516-9086-99bbf2a34078            Anthony Jackson                    elizabeth15@hotmail.com      Electronics           Drug         3              340.46           1021.38          PayPal    2024-12-12       Illinois            43  Female
    404  1ddd1c99-cd9c-4d72-8728-be301133d322               Joshua Price                       ballalexis@yahoo.com             Toys           When         5              121.77            608.85  Mobile Payment    2024-05-09        Florida            46    Male
    405  7acd50db-e073-49f7-8a54-ce1a32c4afbe              Rebecca Drake                    taylormiller@vaughn.org      Electronics         Travel         3               96.92            290.76            Cash    2024-06-04        Georgia            54   Other
    406  e7a495e7-4c45-4d14-a848-ef671923d19a                Mark Waller                      pooleandrew@yahoo.com           Beauty          Range         2              450.12            900.24  Mobile Payment    2024-06-01     California            65  Female
    407  2c7cc0d5-4a60-4ead-9817-573ad64f3f00              Michelle Chen                         sharon27@yahoo.com      Electronics          Small         2              487.45            974.90          PayPal    2025-04-09       Illinois            69  Female
    408  d59f893f-7ebd-4462-9131-6e3530764a0f               Whitney King                        tthompson@yahoo.com      Electronics          Heavy         3              416.86           1250.58      Debit Card    2024-11-02          Texas            64   Other
    409  06f5b9be-530f-4030-8dc6-69a5dcc02b4f              Kathy Sanchez                   kristi58@murphy-rios.org           Sports          Focus         5              307.89           1539.45            Cash    2024-07-06        Florida            40  Female
    410  a3b78551-14bc-47c4-ba9e-5c26a5971271            Joseph Thornton                  andre43@duran-wiggins.org             Toys           Work         3              226.01            678.03     Credit Card    2024-09-25        Florida            50   Other
    411  e9e885d8-dc02-4c4c-8920-32dd20dfc679       Gabrielle Jenkins MD                        martin71@warren.org         Clothing         Option         3              280.50            841.50          PayPal    2024-05-07          Texas            52   Other
    412  a30bfc34-bf4e-4053-a379-813d91d524fb               John Gardner                   chapmanmaureen@yahoo.com         Clothing         Anyone         5              196.78            983.90          PayPal    2024-07-08        Florida            38  Female
    413  6c3c9efa-01b3-4e43-920a-94b73bcb0437               Andrea Perez                        matthew78@yahoo.com             Toys           Wear         2              114.39            228.78          PayPal    2025-05-01       New York            20    Male
    414  6af26d67-01fc-40ba-8e45-393bb72b4e06            Miguel Carrillo                           eric98@gmail.com        Groceries          Worry         2              327.43            654.86            Cash    2025-04-07       Illinois            31    Male
    415  2c025e80-e2b5-456f-81ef-b74e6c260726                 John Miles                  troywilliams@sullivan.com         Clothing        History         1              329.46            329.46      Debit Card    2024-05-22       Illinois            32   Other
    416  4b319e65-d12b-4119-86db-1e4ee917259a               Mariah Clark                      michael74@hotmail.com       Automotive        Include         2               76.49            152.98  Mobile Payment    2024-08-25       New York            53   Other
    417  3907aaec-ddb1-4acb-9573-4c467312b273            Bailey Gonzalez                       dianabrown@gmail.com             Toys             On         5              410.93           2054.65            Cash    2025-01-10     California            25  Female
    418  2a8bd32f-71da-4b8b-9f84-f460e62e58d8            Matthew Cabrera                        garyfrank@petty.net      Electronics           Kind         2              435.92            871.84  Mobile Payment    2024-10-28       Illinois            59  Female
    419  b3308cf8-ea5d-40d9-9f7e-0df0e82640c2          Heather Gallagher       jenniferallen@mcdaniel-guerrero.info             Toys         During         2              435.04            870.08     Credit Card    2024-05-30        Florida            20  Female
    420  833dc70e-1734-4432-b7b3-e3b1d0ca42b7               Tyler Walton                        christy62@yahoo.com           Sports           News         1               48.18             48.18          PayPal    2025-04-03   Pennsylvania            19  Female
    421  c7efab6f-bc27-4856-804b-14e314ef820a              Megan Jenkins                  taylorjames@wade-shaw.net             Toys          Treat         4               86.55            346.20     Credit Card    2024-08-17          Texas            45   Other
    422  c850a446-419f-44a7-aed4-c59ef39502bc         Mrs. Crystal Frost                  paige64@sanchez-burns.com        Groceries          Since         4              464.64           1858.56  Mobile Payment    2024-10-01          Texas            20  Female
    423  79f34093-4a7d-4ccc-bb68-397e080f8baa            Meghan Anderson                           anna72@yahoo.com           Sports        Kitchen         4               11.20             44.80            Cash    2024-11-27     California            30   Other
    424  77cfd17a-606d-4a72-843a-b7978f0b89ce                  Joyce Lin                         qdonovan@gmail.com             Toys        Brother         1              204.65            204.65      Debit Card    2025-04-11        Georgia            43  Female
    425  9a2bbf5e-edc6-4745-9446-1ca88c30a306           Jessica Williams                        laura28@hotmail.com         Clothing       Personal         2              361.33            722.66     Credit Card    2024-12-24   Pennsylvania            64   Other
    426  5c20e427-faee-4314-8d39-c4152f6b3046              John Anderson                webermelissa@christian.info        Groceries         Worker         5              456.16           2280.80      Debit Card    2024-12-10          Texas            53  Female
    427  cfcea07d-e7ed-4910-8ff4-d065d7a26d35             Mercedes Cohen                        erica23@hotmail.com           Sports           Safe         3              223.09            669.27     Credit Card    2024-06-16   Pennsylvania            35    Male
    428  0e3a63d9-a76c-4dd0-a6b7-cf4da3901fbc              Barbara Weiss                   ramosjennifer@dennis.com         Clothing         Detail         4              486.95           1947.80          PayPal    2024-09-17   Pennsylvania            69    Male
    429  5cd47778-7893-4536-9897-0e753ce42811           Charles Lawrence                       jesusmason@ayers.com        Groceries           Need         2              293.08            586.16            Cash    2024-09-16           Ohio            43  Female
    430  37e777c4-82ab-4e5a-90c9-f7b6175026cc          Christopher Avila                    danieldavis@hotmail.com             Home         Finish         5              100.65            503.25            Cash    2024-10-08       New York            64    Male
    431  d5a27c3e-23a0-4f52-baff-5e45491876b2              Angela Rivera                      holtshannon@gmail.com             Toys        Several         5              210.28           1051.40            Cash    2024-12-02          Texas            38  Female
    432  d3532de4-270c-4184-8096-94125a8fd57d               John Jackson                    hansenalyssa@keller.org       Automotive          Along         5               26.88            134.40          PayPal    2024-09-03       New York            27  Female
    433  7b7b6885-ba23-4f1a-941d-1220a68dd9d6          Christina Carroll                     paulkristen@tanner.com           Sports         Sister         5               45.89            229.45      Debit Card    2025-03-30       Illinois            37  Female
    434  ed51fbc1-ceb6-4153-a2e8-af4a36295651               Gabriel Reed                          rtaylor@yahoo.com      Electronics          Might         3              442.81           1328.43      Debit Card    2025-03-13          Texas            25  Female
    435  5e8216bd-304e-4546-9c73-e48f08dbc57a          Jeffrey Rodriguez                         daniel94@yahoo.com        Groceries           Both         5              371.27           1856.35  Mobile Payment    2024-12-31   Pennsylvania            34   Other
    436  12cdb561-e5d4-4f23-8046-a2cd9f594e01               Cindy Deleon                 taylorjennifer@hotmail.com        Groceries         Animal         2              166.51            333.02            Cash    2025-02-10        Florida            31   Other
    437  1069e733-cbf5-4f40-a1d4-5ab2daf24036             Claire Bennett                  wbrown@woods-gonzalez.com           Sports           Cost         1               76.90             76.90  Mobile Payment    2025-03-14     California            25   Other
    438  9a137062-4772-46bf-abad-3adae6fcddc9          Elizabeth Bradley                        nancy07@preston.com       Automotive           Game         1              172.33            172.33     Credit Card    2025-04-13       Illinois            48    Male
    439  d72e1092-cbf0-4476-afc4-4e0f4d8da45f             Shannon Miller                  denisealexander@gmail.com             Home          Check         5               52.78            263.90          PayPal    2025-04-19          Texas            60  Female
    440  9ce7b422-ddab-4dac-bee7-b35dca6c57e0            Michael Maxwell                     ydennis@levy-brown.com        Groceries         Letter         4              474.24           1896.96     Credit Card    2025-02-23           Ohio            56    Male
    441  ab3c221a-95be-42d4-91aa-d929aae2b66a            Angelica Juarez                          yfrench@yahoo.com      Electronics        Husband         5              485.60           2428.00     Credit Card    2025-04-05        Georgia            51   Other
    442  3bd60999-9fc3-4953-bbf5-0b94359ee072                 Jerry Hill                      michelle78@price.info           Beauty         Charge         1              288.50            288.50  Mobile Payment    2024-09-17   Pennsylvania            37    Male
    443  3fcf0b87-ea4e-4911-a856-3ee71f9f8644                 Gina James                     nschneider@raymond.com       Automotive           Face         3               75.55            226.65     Credit Card    2024-10-13          Texas            59    Male
    444  43458a7e-c218-49ca-b97c-5870fb0c7ecc            Michael Jenkins                     kimberly33@hotmail.com             Toys           Left         1              289.45            289.45          PayPal    2024-05-25   Pennsylvania            50    Male
    445  f53af277-897c-4ff5-9519-dc51c2fd954e            Lindsey Burnett                          jacob33@gmail.com      Electronics           Such         2               76.86            153.72  Mobile Payment    2025-03-13        Florida            29   Other
    446  5748c737-44fb-4489-860c-2feaa3090245           Kimberly Clayton                 daniel69@martin-watson.net         Clothing           Head         4              352.63           1410.52     Credit Card    2025-04-10       Illinois            26    Male
    447  350a5b47-e146-4e1a-b501-04964020bdd5           William Griffith                       rturner@mitchell.com             Home            Who         5              352.69           1763.45            Cash    2024-12-09        Georgia            43   Other
    448  a0172447-ecc5-4016-9f8b-193da47a37c3               Laura Nelson                 gonzalezcarolyn@turner.com       Automotive           Tell         4              486.16           1944.64            Cash    2025-03-16          Texas            70    Male
    449  84be37d9-0bad-4338-b000-c61915183c6a            Kimberly Guzman                    nvillarreal@hotmail.com           Beauty       Business         3               69.80            209.40     Credit Card    2025-02-16       Illinois            62  Female
    450  685b6dac-e8e8-495f-ba14-f45a0f877c41                 Renee Ryan                      tsandoval@hotmail.com             Home          Offer         5               89.39            446.95      Debit Card    2024-08-25        Florida            68    Male
    451  d5b13a90-d89f-4b6f-9a2b-042ef2061f78              Henry Sherman                         joshua58@yahoo.com        Groceries          Still         2              115.23            230.46          PayPal    2024-09-08           Ohio            35   Other
    452  aaa3885d-3ecd-4fcf-8a95-e68f98341726             Tyrone Parsons                    gonzalezsarah@yahoo.com      Electronics          Often         1              254.74            254.74            Cash    2025-03-20       Illinois            66  Female
    453  ec1b31cd-bbdf-43a6-bcce-33ef0855d169            Daniel Richards                     millermichael@dyer.net           Beauty            Run         3               44.75            134.25      Debit Card    2024-07-29       New York            29    Male
    454  b757a1be-6e35-47c7-af0f-9ba65034d4f6        Christine Patterson                     gordonandrew@gmail.com        Groceries         Appear         5              387.25           1936.25     Credit Card    2024-08-13          Texas            35   Other
    455  97bf5fb7-a10b-4dcc-96e5-290887c25ca0            Vanessa Alvarez                     rebecca91@mitchell.com             Toys           Here         2              128.09            256.18  Mobile Payment    2024-10-29     California            47  Female
    456  53036e2c-d402-42aa-a478-86812d586a62             Sean Henderson                       wdeleon@gonzalez.com             Home           Many         5              230.17           1150.85          PayPal    2024-09-25        Florida            67   Other
    457  0e70150d-16eb-4ba5-9098-750536924c98                Erica Stark                gillespiejustin@hotmail.com         Clothing          Small         3              335.34           1006.02     Credit Card    2025-04-12           Ohio            66  Female
    458  8f2ffd0f-58ce-45c0-b199-5d76909be479                Pamela Ruiz                     mitchell01@hotmail.com         Clothing          Spend         4              118.14            472.56            Cash    2025-02-07       New York            44   Other
    459  6a60086a-18a1-4576-a761-f297c51bd66d              Richard Baker                         lfisher@barron.com             Toys           Road         1              132.07            132.07          PayPal    2024-12-12          Texas            47   Other
    460  745ca9a8-d406-49cd-9e35-c3873da4e2d3              Brenda Warren                          zhaynes@gmail.com        Groceries           Work         5              134.00            670.00          PayPal    2024-07-10          Texas            59   Other
    461  64b41bd5-2c10-4069-98ad-a575ce3ba364              Justin Wilson                      austin08@robinson.com        Groceries       Evidence         2              206.69            413.38      Debit Card    2025-02-18       Illinois            47  Female
    462  46eef48f-ca50-4921-9ddd-709ba438bd75              Jodi Bartlett                        burnsalan@gmail.com         Clothing         Change         5              280.60           1403.00  Mobile Payment    2025-04-26   Pennsylvania            65  Female
    463  8f37e8fe-0530-4898-ae1a-b80bc6944e99               William Howe                      hansenjenna@rice.info             Home        Evening         3                5.89             17.67  Mobile Payment    2024-10-04       New York            47   Other
    464  081cdf29-c986-4bde-80c0-162516e5d3b8                Alison Meza             johnsonmary@anderson-ellis.biz           Sports        Because         4              348.86           1395.44     Credit Card    2024-09-09          Texas            49   Other
    465  8c9082a3-947e-40e0-a239-9974924bba5d               Michelle Ray               maysmichelle@berry-jones.biz           Sports          Third         4               89.69            358.76            Cash    2024-10-18           Ohio            50  Female
    466  87eae472-d79c-4f96-9fed-9a7de64f30c7               Shawn Parker                      katherine19@gmail.com           Sports            Now         3              439.90           1319.70            Cash    2025-04-10          Texas            33    Male
    467  b67deac1-fdba-4dfb-8dd3-c1e78cb1c287               Bailey Young                            kruiz@gmail.com             Home        Several         1              203.99            203.99  Mobile Payment    2024-10-27     California            57  Female
    468  73625409-5c13-4401-84cb-ce831751bdc3             Bruce Melendez                   campbelllarry@nguyen.com             Home           Here         3              180.52            541.56  Mobile Payment    2024-08-17           Ohio            40    Male
    469  796cdcba-afa4-4a63-bc34-ae5a8653d681              Amber Gregory                          derek41@gmail.com        Groceries          Check         3              338.67           1016.01      Debit Card    2025-01-06       New York            68    Male
    470  9fab12cd-7281-429d-80c2-dfdb45fb015b              Matthew Weeks                      gillandre@hotmail.com             Toys          Prove         5              313.11           1565.55          PayPal    2024-05-16        Georgia            21   Other
    471  04231ba1-74cc-4ec0-b26b-f3e5d4f7cc55                Jack Flores                   hallison@olson-baker.com      Electronics         Wonder         3              342.78           1028.34  Mobile Payment    2024-07-02   Pennsylvania            44    Male
    472  84837376-5f81-442f-b5cb-6e8ba2538230             Michael Garcia                    cherrymichael@gmail.com        Groceries     Democratic         4               34.61            138.44      Debit Card    2024-06-05       Illinois            26  Female
    473  3875c317-79c0-412b-b002-0ff362aeb1a4               Tony Leonard                     bateswendy@vazquez.com         Clothing           Same         3              132.59            397.77            Cash    2025-02-01   Pennsylvania            32    Male
    474  b95ec357-52aa-418b-be87-a90bc5ea96df         Miss Valerie Braun                   brandongomez@hotmail.com             Home           Fish         1              408.47            408.47  Mobile Payment    2025-04-04          Texas            38   Other
    475  50c0de3f-0cca-45b4-ad32-0159172ed006           Kristopher Lopez                  karlmcfarland@hotmail.com        Groceries           West         2              417.96            835.92  Mobile Payment    2024-12-12        Georgia            49   Other
    476  511b3884-1957-4723-833b-e2172fbc1347            Michael Shields                    cookbarbara@hotmail.com             Toys         Effort         2               45.53             91.06      Debit Card    2024-05-05        Georgia            40   Other
    477  fbdec6f6-8898-437e-b2e9-5ad08968bca3               Kathy Kelley                             bray@bell.info         Clothing          Stuff         4              213.12            852.48            Cash    2025-04-17          Texas            47   Other
    478  fb6157b4-5b06-4658-8131-c113fc324465            Leslie Castillo  mclaughlincourtney@jennings-marshall.info        Groceries            One         1              138.37            138.37          PayPal    2024-10-23        Georgia            65    Male
    479  e69b1332-a45a-4a29-9b9f-09df6d012f60                Michele Fry                richardsonwesley@dudley.net         Clothing           Call         2              207.09            414.18     Credit Card    2025-02-15        Florida            34    Male
    480  91b2a4a8-f59d-4548-b426-b1a98cc3ae6c             Michael Barron                 adampatterson@williams.com      Electronics      Interview         1              444.79            444.79      Debit Card    2024-09-11           Ohio            28  Female
    481  0d2dd323-7a3b-4129-abd1-b548249b45e3              Sharon Wilson              mahoneymary@lucero-castro.com             Toys          Reach         1              213.33            213.33          PayPal    2024-11-05     California            44  Female
    482  12098941-9119-4ad5-94a3-c82abdebaa40              Darrell Kline                    jonesbenjamin@gmail.com             Home        Teacher         1              258.50            258.50          PayPal    2025-01-01   Pennsylvania            53   Other
    483  0e5a009b-076d-4c82-9818-40463fb3ac1c                Rick Wilson                     holderallen@turner.com      Electronics        Culture         4               67.91            271.64            Cash    2024-07-04   Pennsylvania            66   Other
    484  b20846e1-6045-40d6-991c-1e7f24341021               Brian Nelson                         jperry@hotmail.com             Home        Account         4               27.34            109.36  Mobile Payment    2025-02-28   Pennsylvania            41  Female
    485  be7b203b-9361-496e-90f9-dc3756acdc10                Megan Gomez                     racheldixon@miller.org             Toys          Heart         5              242.72           1213.60            Cash    2024-06-20       Illinois            40    Male
    486  22c8fe02-a475-4a2d-b326-46d9efe232af                Andre Moore                              lpark@ray.com           Sports           Fact         4              338.61           1354.44            Cash    2024-05-06          Texas            65   Other
    487  5d2c8c2c-c277-42e9-b21c-989964cfb670            Samantha Zamora            jacksonsullivan@weaver-hall.biz             Toys           Rule         1              392.48            392.48            Cash    2025-04-28        Florida            39   Other
    488  4f478217-8b67-432b-99b3-22b0190745e0            Katrina Delgado                     teresaturner@allen.org           Sports          Laugh         3              160.42            481.26          PayPal    2024-12-02          Texas            64  Female
    489  9cbf83f9-9ae2-4544-b123-73f744043ea1        Christopher Escobar              jennifer55@church-rosales.com             Home         Strong         4              134.08            536.32          PayPal    2024-07-26        Georgia            55    Male
    490  c395dcad-177e-4f41-b33e-b4da402b10b4               Michael Lynn                          qwillis@perez.com      Electronics      Community         2               45.44             90.88     Credit Card    2024-10-27          Texas            46   Other
    491  ce578277-38cb-4ad2-8ce8-4f3bebd55290              Lisa Mcdonald                      josephsmith@yahoo.com             Home            Off         4              305.61           1222.44          PayPal    2025-04-01           Ohio            25    Male
    492  cd2a0864-463b-47c9-9bd6-a8a6ea379a65            Michael Watkins                         ariana02@yahoo.com           Sports          Plant         1              383.12            383.12      Debit Card    2025-03-23     California            56   Other
    493  d6dc2ea4-d556-4e94-aec1-db5932343bb0                Ian Mullins                       travis33@hotmail.com             Toys         Couple         1              235.49            235.49            Cash    2024-08-17        Florida            27  Female
    494  1e04ae4f-e65f-4b42-92f8-e2836618d910            Rachel Phillips                stevenramos@davis-lloyd.com         Clothing           Pick         5              221.08           1105.40          PayPal    2024-10-05          Texas            59   Other
    495  44de8326-633a-4a7f-a531-dc9dc810bd42         Angelica Velasquez                     tiffanyzhang@curry.org         Clothing            Bed         2              434.31            868.62     Credit Card    2025-04-17          Texas            49    Male
    496  7785dd9d-20ae-4eaf-8b63-1b4fbb5c22a8             Patricia Lewis                      gthompson@hotmail.com       Automotive         Memory         1              316.52            316.52     Credit Card    2024-10-09        Florida            34  Female
    497  d86a77d4-97f8-49a0-ad89-55f5332445fe               Joseph Lucas                    elizabeth91@hotmail.com             Home          Ahead         5              415.22           2076.10     Credit Card    2024-12-12           Ohio            69  Female
    498  d5a9bb62-d155-4d1e-b730-e9cbd81199bd              Daniel Church               elizabethdavis@mcdonald.info         Clothing          Phone         5              190.13            950.65      Debit Card    2024-12-19       Illinois            43    Male
    499  9df49f1c-5354-42df-be78-6f94a7228bda              Rose Guerrero                            bsnow@dixon.com       Automotive           Page         3              360.32           1080.96      Debit Card    2025-01-03   Pennsylvania            64    Male
    500  e61d5960-fe91-44a5-a953-851abda77649               Robert White              samantha31@mitchell-brown.com      Electronics        Reflect         3              121.73            365.19          PayPal    2025-03-30     California            55   Other
    501  8d35a17c-c7bd-4e30-b5d0-60fdccdb273f               Carol Carson                    jamierobinson@yahoo.com         Clothing       Majority         4              420.45           1681.80     Credit Card    2024-09-13     California            34  Female
    502  f5e4cc02-5bd9-4511-af72-470d5981f8e4                Susan Haley                   rjohnson@smith-avery.com       Automotive           Rule         2              421.21            842.42            Cash    2024-08-30           Ohio            52    Male
    503  9dba4eae-a566-4d45-a01a-81e56a81584a               Willie Ortiz                        osantos@hotmail.com             Home        Citizen         4              486.70           1946.80      Debit Card    2024-09-15       Illinois            23    Male
    504  90fcfcb7-16ea-425b-9e1a-17653830842e                 David Ryan                          janet53@gmail.com             Toys           Wear         1              297.86            297.86            Cash    2024-06-13       New York            54  Female
    505  c092668a-777c-4bf1-96e9-fd2ada0cb9ef            Sheena Griffith                    andrewhammond@yahoo.com             Home           Dark         5               84.00            420.00            Cash    2024-06-03       New York            41  Female
    506  dd268b6c-f16f-4ccd-98d1-696d72a11f61                Kevin Banks                          bclarke@gmail.com         Clothing        Someone         3              167.04            501.12            Cash    2024-12-19       Illinois            37    Male
    507  552493b7-8d41-430c-9e81-2d73a7354b7a            Candice Coleman              jennifer23@flores-pearson.com             Home        Product         5              332.41           1662.05          PayPal    2024-10-31          Texas            21    Male
    508  bdf7b9af-8587-447c-87a0-3c4a47f7e404              Emily Burgess                        ethan05@bennett.biz             Toys           Rock         4              397.36           1589.44            Cash    2024-05-30       New York            24    Male
    509  55bf9ca9-35dd-43c3-89f4-4ab3b9db13b4             Heather Hardin                        crystal94@gmail.com        Groceries     Democratic         2              366.72            733.44            Cash    2024-05-06        Georgia            56   Other
    510  2895b3cc-7f8f-4150-a34a-e8f2451fdf0f               Ronald Brown                             tstone@ray.com           Sports         Leader         5              199.27            996.35            Cash    2025-02-09       New York            54    Male
    511  6ea21c25-fa86-4dee-a549-53962389693e               Brenda Quinn                   williamsadam@church.info       Automotive         Toward         5               91.98            459.90          PayPal    2025-04-23          Texas            54   Other
    512  61172ed6-e1f2-4186-a59f-56e887b29f38                 Anna Lynch                           gsmith@yahoo.com           Beauty           Tell         5              199.64            998.20     Credit Card    2024-07-21       New York            56   Other
    513  36d01b43-d278-4d89-a4f5-2f7777ba2d21               Joseph Brown                          tbranch@lewis.org             Toys        Require         4              362.58           1450.32          PayPal    2025-02-02           Ohio            53    Male
    514  0af475f4-729f-43b4-b20d-da6f1895d72e               George Lynch                        derrick92@yahoo.com       Automotive          Ahead         2              335.66            671.32     Credit Card    2025-02-04        Georgia            58  Female
    515  67939266-41d5-4d65-8710-29fa6b14e139                 Maria Chan                      nicolerivera@reid.net             Toys  International         3               22.12             66.36            Cash    2025-02-07        Georgia            23   Other
    516  73402e90-a0f7-4c69-b107-551f386d8e28                Tonya Moore                 howedawn@andrews-jones.biz       Automotive          Small         3              363.73           1091.19     Credit Card    2024-12-28     California            37  Female
    517  2a78d218-a89f-4432-a6ef-dbf4617e727b            Joshua Friedman                   austinrussell@ibarra.com         Clothing         Career         1              415.39            415.39  Mobile Payment    2024-11-06     California            28   Other
    518  d4bc1c92-27dc-442c-8610-4516810a6a7c              Ryan Thompson                          grant22@gmail.com             Home           Push         2              367.19            734.38            Cash    2025-01-25       Illinois            22    Male
    519  eec316c2-6d0f-4ee9-a4eb-235e205d6651             Michael Knight                      vwilliamson@yahoo.com             Toys        Success         5                5.32             26.60     Credit Card    2024-10-06           Ohio            26  Female
    520  0e64e865-15da-4b18-b1f6-0b51757e3601            Victoria Conley                    wattsnicholas@gmail.com      Electronics      Difficult         1               15.31             15.31            Cash    2024-11-03          Texas            37    Male
    521  5b870767-d4ed-4232-9caf-3d31824d004e               Barbara Reed                         erin75@hotmail.com         Clothing           Race         5              320.93           1604.65      Debit Card    2024-08-29       New York            37  Female
    522  cd57fafe-6ad0-4a8e-b0db-5421f637ee58              Crystal Lewis                         isabel48@gmail.com           Sports           Part         2               53.73            107.46          PayPal    2025-04-20          Texas            47    Male
    523  50cd9537-d7d6-4cd3-a32c-15d36aab9dce                Teresa Shea                     scase@yates-miller.com        Groceries    Institution         1              457.28            457.28            Cash    2025-02-02        Georgia            27  Female
    524  3913d31d-5a22-4703-b3e5-d994a50fdb9c              Michael Smith                   buchanandaniel@gmail.com        Groceries           Save         4              165.68            662.72          PayPal    2025-02-10           Ohio            66    Male
    525  adc67fe2-70a1-492b-931e-187a1267a0c7              Jonathan Neal                         qjimenez@yahoo.com       Automotive         Growth         1               40.07             40.07            Cash    2025-02-03   Pennsylvania            33    Male
    526  f5ede630-007f-471c-8099-e0709e67be50               Jason Holmes                   sphillips@villarreal.com           Beauty         Police         2              324.23            648.46            Cash    2024-07-08          Texas            48    Male
    527  63450b69-21ed-4fa2-bf40-fc72068667fe               Paige Stuart                     ashleyhansen@yahoo.com         Clothing       Possible         4              183.56            734.24      Debit Card    2024-12-15       Illinois            36    Male
    528  f7a5a3a3-c3ac-4c0c-b3b7-312c0eaae312                Rachel Cook                           vblack@yahoo.com        Groceries      Statement         2              248.91            497.82      Debit Card    2024-05-28   Pennsylvania            31   Other
    529  b15cf527-10d3-4f9f-a49a-6c25b57a5ef8                 Ryan Young                      jasmine44@barnett.net        Groceries       Majority         4               13.00             52.00            Cash    2025-04-30        Florida            31    Male
    530  f0797b8f-1c52-4ab8-b4af-3e65432467c2           Jennifer Roberts                courtneyroberts@hotmail.com        Groceries          Start         3               18.50             55.50            Cash    2025-03-19   Pennsylvania            20   Other
    531  3a0b2013-f461-4c8f-9795-01c97cbd92cb         Christine Wade PhD                     meyersgina@hotmail.com             Home         School         2              297.38            594.76  Mobile Payment    2024-12-26   Pennsylvania            70  Female
    532  b4571747-6ebb-4291-81aa-f9f1960d91f0          Katherine Johnson                cthompson@hawkins-baker.org       Automotive           Huge         2              407.16            814.32     Credit Card    2025-03-08        Florida            58    Male
    533  919e7476-6177-48e2-911a-908bb13a9b7a              Mario Ballard                        michael85@mason.org           Beauty          Teach         4              132.34            529.36            Cash    2025-02-26     California            32   Other
    534  200aba7f-8aa6-4827-b73e-0645891524a9              Connor Conner                 renee66@butler-jackson.com      Electronics        Nothing         4              498.68           1994.72            Cash    2024-12-20       Illinois            54    Male
    535  44b4fa91-e67e-47f7-9942-b8e405d3e773               Sherry Jones                       curtis35@hotmail.com       Automotive          Right         5              476.32           2381.60            Cash    2024-08-25          Texas            58   Other
    536  3ae95dca-5deb-4199-a638-8fcb5a2a57dd               Robert Scott                schmittclifford@russell.org       Automotive           Fall         2              391.45            782.90  Mobile Payment    2024-11-17       Illinois            55    Male
    537  4696b6cf-7d06-4d29-afc3-55005885a638              Beth Williams                           xbrown@marsh.com             Home            Six         5              199.32            996.60  Mobile Payment    2024-10-02       Illinois            34   Other
    538  1ce5e77c-98f4-43e4-a33b-8787b7b3d608               Kevin Wilson                    veronica46@mcdowell.org           Sports          Whose         2              166.76            333.52            Cash    2024-10-31          Texas            25  Female
    539  9100982d-6609-448b-a2a7-7d148371262e              Robert Larson                         beth38@hotmail.com         Clothing        Century         4              358.40           1433.60  Mobile Payment    2024-09-18       New York            32    Male
    540  f5eca2dd-a350-4e8c-b311-a8c0aeffcd19            Victoria Fisher                      jwilliams@hotmail.com      Electronics           Fill         2                9.98             19.96          PayPal    2024-07-29          Texas            58  Female
    541  498b5812-6e70-44f2-8e88-e945300d5a6b                Amanda Hill                       cheryl98@gilmore.net             Home        Measure         3              304.68            914.04      Debit Card    2024-06-22       Illinois            22   Other
    542  d90511ad-9883-4ede-afca-2338db61864c             Caitlin Nelson                     romeroedward@yahoo.com             Toys           Head         2              479.01            958.02      Debit Card    2024-09-24        Georgia            39  Female
    543  547356ea-6e7d-47b4-b864-d2e5254b05ad        Veronica Cunningham                    deanpadilla@hotmail.com             Home         Rather         3              296.45            889.35  Mobile Payment    2025-03-11   Pennsylvania            18   Other
    544  f696a04e-7969-4096-a742-48313fb9e897              Angela Cherry                     brittney43@hotmail.com        Groceries       Customer         5              278.31           1391.55      Debit Card    2024-09-26       New York            69   Other
    545  0766784e-19a0-4d45-bc75-b99161d3acac              Douglas Woods           nathaniel37@ballard-anderson.com           Sports        Capital         2              439.25            878.50            Cash    2025-01-19     California            20    Male
    546  59d768e1-7748-4188-ac71-3d5681ae6b42          Christian Watkins                       brianbailey@soto.com           Sports           Hour         1              355.02            355.02      Debit Card    2024-09-01   Pennsylvania            62    Male
    547  79dab2bb-12fc-4afb-91f2-794760768c9c                Victor Wood                   williamsdaniel@yahoo.com           Beauty       Suddenly         1              138.53            138.53            Cash    2024-11-12     California            63    Male
    548  5f5ce531-29a2-464b-87da-f88c45dceede          Mrs. Kayla Pineda                  dillonmurillo@hotmail.com           Beauty           Show         4              349.77           1399.08     Credit Card    2024-09-09   Pennsylvania            56  Female
    549  44f89a26-a191-45db-9e98-644e653c73ad                Laura Lewis                  williamskelly@hotmail.com             Toys          Offer         4              359.92           1439.68      Debit Card    2025-04-23   Pennsylvania            26    Male
    550  13521c52-3e10-46e6-af96-dbe1152e50d9             Deborah Cortez                         stacey48@yahoo.com             Home         Figure         2              145.36            290.72     Credit Card    2025-02-18     California            70   Other
    551  ef0fc299-997f-4022-8f9a-11134d1f6f55              Richard Greer                   ramirezmichael@gmail.com        Groceries           Ever         5              498.62           2493.10     Credit Card    2024-05-05       Illinois            38    Male
    552  5096796d-89f0-470a-83b5-3f23668cb1a8                Tyler Smith                           paul16@leach.com             Toys        Station         5              196.55            982.75            Cash    2024-06-02        Florida            40   Other
    553  75f9e978-7244-4be0-90ae-ee771b76730d                Calvin Koch                underwoodlucas@fletcher.com      Electronics           From         2              267.05            534.10          PayPal    2024-07-25        Georgia            61   Other
    554  6d25fe49-c955-4639-a3a7-0397f3f82c61              Joshua Snyder                     kathleen13@hotmail.com         Clothing      Situation         1              120.49            120.49     Credit Card    2024-11-02     California            64  Female
    555  1e7985ef-741e-4437-a81d-bf7e7311e863            Raymond Rowland                          tdodson@brown.com             Home    Opportunity         2              286.31            572.62            Cash    2025-04-28          Texas            30   Other
    556  a61a596a-82e0-4492-91ea-b07357663fc8             Alexander King                           sfoley@gmail.com       Automotive           Plan         4              345.07           1380.28          PayPal    2024-08-26        Florida            28    Male
    557  17f5d492-d19f-4551-9663-814cd059cd3a              Michael Mejia                         ylopez@hotmail.com      Electronics           Test         3              400.62           1201.86          PayPal    2024-08-12     California            49   Other
    558  a5764db1-5c02-482d-9d07-057a4a068d1c               Melinda Ruiz                         uprice@hotmail.com      Electronics           Fill         1              272.20            272.20          PayPal    2024-10-04   Pennsylvania            20    Male
    559  dfe9c727-77a6-4346-b2f2-9c2a16e77325                 Mason Ward                      petergreen@harvey.net           Sports           Wind         1              216.40            216.40      Debit Card    2025-02-21     California            53    Male
    560  192bbc2f-82b0-4852-9787-b3b71fd8ad68                Tim Daniels                      andrewhayes@yahoo.com        Groceries           Rate         4               90.06            360.24            Cash    2024-07-19        Florida            62   Other
    561  40ced57f-a480-4e9c-bdac-3df6ec6b547e                 Amber Hall                        melissa10@yahoo.com             Toys          Black         4              480.79           1923.16          PayPal    2025-02-26        Florida            34  Female
    562  5d68951a-c4bc-454f-a1ea-955f0ee8ecd0              Linda Manning                  chad68@gomez-gonzalez.com      Electronics          Class         5              426.94           2134.70  Mobile Payment    2025-04-29          Texas            34  Female
    563  064591e6-4ecd-4fba-bdff-89fa9880596f                Evan Turner                        mrobinson@gmail.com        Groceries          Scene         5              474.39           2371.95  Mobile Payment    2024-05-16     California            58   Other
    564  8957311a-86da-482d-bf83-5e53861fb228               Karen Carter                    zespinoza@anderson.info             Home             Mr         5              476.73           2383.65          PayPal    2025-01-17   Pennsylvania            45  Female
    565  79002e41-da60-49c2-bfe4-445dcf7bd35f           Christine Gordon                 stephaniebooth@hotmail.com           Sports          Raise         1              132.35            132.35     Credit Card    2024-08-13       New York            36  Female
    566  da8b0e4d-79fb-4c66-bdd3-2075370b640c              Tracy Johnson                    debra62@munoz-jones.net         Clothing            Ask         4              433.20           1732.80     Credit Card    2024-08-02           Ohio            51  Female
    567  af1aebdd-49a4-4998-87ba-0eb2bff7d2d7                Roy Jenkins                           twalls@gmail.com           Sports            Art         3              109.20            327.60          PayPal    2024-12-12       New York            31  Female
    568  11f42e8b-c97d-4760-bf0c-260555b7e398         Michael Richardson                           hknapp@gmail.com        Groceries           Fall         5              337.67           1688.35      Debit Card    2024-08-27   Pennsylvania            24    Male
    569  35192826-280c-432a-a1d0-275970b0ebb0                  Brett Lee                       brodriguez@yahoo.com         Clothing    Institution         1              101.75            101.75     Credit Card    2025-03-12          Texas            30    Male
    570  ab55dc09-4cc2-4fa3-a118-ad3a1c3a51d8              Anthony Floyd                cwalker@mclaughlin-wood.com      Electronics        Popular         3              137.43            412.29     Credit Card    2025-01-28        Florida            54   Other
    571  1ce7f3a3-c4ca-49f2-ab87-9393474f41e5              Kristin Henry                        asharp@delacruz.biz           Sports           Able         2              402.12            804.24            Cash    2024-12-14       Illinois            26    Male
    572  e2bc374e-ea9e-4a78-bf23-71f8bc54199e            Katelyn Nichols            mcdanieljacob@edwards-flynn.com         Clothing           Next         3              203.21            609.63      Debit Card    2024-06-09     California            24   Other
    573  9d32dc48-b14a-4504-91e3-a2767f608e8b             Virginia Young                           bsmith@gmail.com           Beauty       Majority         3              365.47           1096.41  Mobile Payment    2024-11-12     California            53  Female
    574  887490cf-2531-4905-9350-b9362035cbc2               Cindy Austin                          wayne16@gmail.com        Groceries         Window         1               36.95             36.95     Credit Card    2025-03-26           Ohio            24  Female
    575  2a1e8b8a-c501-45e7-9781-449c2ae3a7b4            Sarah Armstrong           baileybrenda@clark-rodriguez.org           Sports           Pick         5               45.64            228.20          PayPal    2025-03-29          Texas            52  Female
    576  0cb587ab-8c45-4dc3-94d0-f5a1e995f26f               Daniel Brown                    kberg@dillon-norris.com         Clothing        Require         5              382.81           1914.05            Cash    2025-01-19          Texas            31  Female
    577  fa99b517-559b-4399-9783-48a8e9e86627               Cheryl Adams           carrieramirez@branch-jackson.com             Home          Often         3              466.58           1399.74            Cash    2024-11-24       New York            38   Other
    578  f925b441-5d54-4c33-8335-d8ed36389d08              Michael Riley                        susan52@hotmail.com      Electronics         Rather         2              303.93            607.86            Cash    2025-02-08   Pennsylvania            25    Male
    579  1d1a816d-2955-4549-b337-4257a95e1892            Patricia Morgan                 nicolerichardson@gmail.com        Groceries           Time         4              252.10           1008.40          PayPal    2025-01-31        Georgia            48   Other
    580  e2778ac7-bcb0-482c-b1f8-a42c58bd4c3b                 Julie Hays                  evan39@morales-martin.com       Automotive      Important         1              443.43            443.43     Credit Card    2025-02-22          Texas            38   Other
    581  15f28ca5-cf91-4757-ae5e-a9061e60a269              David Mueller                        olsonlisa@yahoo.com           Beauty           Rock         4              307.55           1230.20  Mobile Payment    2024-07-20        Georgia            68    Male
    582  c396454b-8420-4085-b02d-661f52714a05              John Callahan                         ngarcia@austin.net       Automotive             Me         1              238.18            238.18     Credit Card    2025-04-06           Ohio            26    Male
    583  76423463-32db-4fba-8f5e-e128b767c043              Rachel Wilson               oliverheidi@riggs-miller.com             Home        Student         1              395.87            395.87      Debit Card    2024-10-26        Georgia            66   Other
    584  544f7b76-0a02-419a-aa23-8794730cf958                John Wagner                     travisbeck@hotmail.com           Sports           Upon         5               88.58            442.90            Cash    2024-07-26          Texas            46   Other
    585  bf41dcb3-19c6-495d-a4bc-2988ede56bd9                 Shaun Gray                     davidmoody@hotmail.com       Automotive          Party         4              115.41            461.64  Mobile Payment    2025-02-19       Illinois            51    Male
    586  db1a9bfe-9fbf-4b88-9e20-a75b1cffdafe           Samantha Camacho                   marshkevin@vega-webb.com         Clothing          First         2              457.49            914.98  Mobile Payment    2024-09-26        Florida            18    Male
    587  47a8dd28-1fe8-4409-9259-a32e9b34a97e               Travis Smith                      duncandanny@brown.net           Beauty          Field         2              446.85            893.70          PayPal    2024-09-05           Ohio            31  Female
    588  2af9aefe-6424-4700-a394-8491a2bcbe11               Jason Conner                           john72@noble.com        Groceries           Unit         4              209.70            838.80      Debit Card    2024-06-15           Ohio            44    Male
    589  becfb4e3-0e2e-4634-bbe1-e6c7de62e919              Robert Brewer                       destrada@russell.net           Beauty           Only         1              180.97            180.97  Mobile Payment    2024-05-16        Georgia            37  Female
    590  985e4714-8bb4-42bf-a44e-601aae7aa0ab             Samantha Lynch          douglasjoseph@hamilton-wells.info           Sports         Across         3              293.94            881.82          PayPal    2024-12-15        Florida            55    Male
    591  7b0019ec-5249-4668-8491-7f09b544769b                 Jose Dixon              marymoreno@hartman-porter.com        Groceries          Large         1              326.18            326.18      Debit Card    2025-02-26     California            31    Male
    592  acbb71bc-aa86-4d74-b74e-c8599ff4dd27              Steven Harmon                     ayalacrystal@gmail.com      Electronics         Father         2               29.19             58.38      Debit Card    2025-04-12       Illinois            42  Female
    593  12110e6f-5ff5-4d59-8f26-36b49f347c62                 Jason Hill                     barbara45@gonzalez.com      Electronics            Car         2               93.64            187.28     Credit Card    2024-08-29   Pennsylvania            55  Female
    594  b950432e-b9e9-4eaa-b477-4404499e3d86              Robert Wright                        maria03@hotmail.com        Groceries         Memory         4              296.12           1184.48      Debit Card    2024-05-09           Ohio            51    Male
    595  c00b788d-2979-49be-ac4c-1d0f04bce119            Kimberly Conley       wilsonsamantha@brooks-washington.net         Clothing        Economy         1               56.71             56.71          PayPal    2024-12-17          Texas            25    Male
    596  cccf7a35-6f87-4ac1-9b27-5f23a9d865f0             Katie Mckenzie                     kingbrittany@yahoo.com        Groceries          Enjoy         3              377.40           1132.20  Mobile Payment    2024-06-20        Florida            45    Male
    597  d26d7139-02ca-4b77-936b-7d9f2c26a96c              Kristin Brown                   aaronkennedy@hotmail.com         Clothing            Mrs         4              438.71           1754.84      Debit Card    2024-06-28       New York            35   Other
    598  a56611dc-d07e-4190-a27b-e8618b6a1ac9           Raymond Jacobson                          carol94@gmail.com      Electronics        Tonight         1              353.46            353.46            Cash    2024-08-08   Pennsylvania            32    Male
    599  f013e475-23f8-4561-8a5c-9b28b01d0234                Chris Jones                       mmeadows@hotmail.com           Sports        Mention         5              270.61           1353.05     Credit Card    2025-03-11   Pennsylvania            69   Other
    600  875c9d5f-3092-4b45-95e5-11bd629bc68d            Alexander Jones                millerdorothy@rodriguez.com             Home       Everyone         5               78.63            393.15      Debit Card    2024-12-19        Georgia            21  Female
    601  d1a3c17a-faad-489c-be2a-9a5a74a1ed82            Allison Osborne                      myersrobert@yahoo.com           Sports            Law         1              118.80            118.80            Cash    2024-09-28          Texas            43    Male
    602  2d269687-8c44-4ffd-b597-a41a146994e2            Kristin Leonard                      miranda58@hotmail.com           Sports      Professor         1               83.20             83.20      Debit Card    2024-12-12       Illinois            67    Male
    603  f8ecb094-2d44-4ace-830b-2f7d6f86e4c0                   Juan May                crystalwatson@gutierrez.com             Toys         Speech         1              292.64            292.64  Mobile Payment    2025-02-12          Texas            23   Other
    604  5bc46987-db8c-49c6-ac5a-ac48104f0ece                Joseph Hays                         sandra18@yahoo.com             Home           From         3              258.24            774.72  Mobile Payment    2024-06-06          Texas            20    Male
    605  8e559ea7-3e61-4ecc-8d28-ab40a7f4a9cb                Susan Young                         meagan02@yahoo.com         Clothing         Garden         5              220.83           1104.15            Cash    2024-08-22           Ohio            56    Male
    606  58810e0e-4d39-4f0b-a3fc-a5b2925af298             John Rodriguez                       ericmiller@gmail.com           Beauty           Talk         1              490.33            490.33  Mobile Payment    2024-06-01   Pennsylvania            51    Male
    607  d3caedfc-05bd-4317-8362-aa57eeadbeb4              Jessica Terry                        jeffrey69@gmail.com           Beauty         Policy         1              332.08            332.08          PayPal    2025-04-12          Texas            68   Other
    608  3204c57d-2adb-4fd6-aa8b-24a8b6a8edca               Judy Solomon                      omarcarroll@gmail.com             Home           What         5              344.34           1721.70          PayPal    2024-09-14     California            25    Male
    609  3f3806a3-42ee-4d1f-8606-8356caf2db55               Jose Rollins                            adean@yahoo.com      Electronics        Success         4              145.71            582.84          PayPal    2024-05-15           Ohio            70    Male
    610  558f6f54-0b3f-4d75-beab-cb37940fc364             Kimberly Davis                      amypaul@reid-pena.com             Toys        Another         4              451.24           1804.96          PayPal    2025-04-19   Pennsylvania            50  Female
    611  713f403b-8bf3-4b99-929e-5ec50afb8bd8                Bonnie Cole                    jasonmorgan@barnett.com           Beauty         Health         4              290.51           1162.04      Debit Card    2025-03-07        Florida            28   Other
    612  bdb268e3-b353-4ad3-8b48-65feda66b1ef                Bradley Fox            scottaguirre@holland-taylor.com             Toys         Figure         3              280.02            840.06          PayPal    2024-07-17     California            28   Other
    613  3b6ef751-5b99-4c4b-abf5-99515579144f              Vernon Becker                         vincent31@rios.com      Electronics          Adult         1               27.10             27.10            Cash    2025-02-22        Georgia            53    Male
    614  effcea7e-58e1-4935-b0bb-3568f0bb6472                 Holly Carr                            eric97@bush.com       Automotive       Question         2              117.73            235.46            Cash    2024-06-20       New York            31   Other
    615  e57b559f-5e32-4699-a527-8a4b96436e85              Terry Goodwin                      jacobwalton@davis.com         Clothing     Technology         1               97.70             97.70          PayPal    2025-03-13     California            30   Other
    616  d982b942-571d-47cc-900e-7dca61986a75                 Jose Moore             biancawheeler@moore-smith.info      Electronics     Especially         5              479.93           2399.65            Cash    2024-10-26       Illinois            41   Other
    617  cd94ffb5-cdda-4126-a89b-562e55bc0f16             Kevin Jennings                       joseph51@perkins.biz         Clothing          There         5              322.05           1610.25      Debit Card    2024-10-25   Pennsylvania            36  Female
    618  682252b5-f69b-4239-ba9f-39814163f033              Carlos Sparks                        qfuller@hotmail.com           Beauty           Send         4              185.92            743.68            Cash    2025-03-12     California            19   Other
    619  94da9139-2a1d-419e-bd33-fac6036ea578                 John Keith                 barronrobert@rodriguez.com       Automotive            Kid         4              293.27           1173.08      Debit Card    2024-05-02     California            51   Other
    620  87f96cf6-cfa7-41c0-bd4e-af0ce18ab0ad              Charles Lynch                     bhansen@valenzuela.net           Sports           Huge         5              220.08           1100.40  Mobile Payment    2025-01-10           Ohio            28  Female
    621  04db301d-735e-4e9b-86af-4a460f5c2b50          Brandi Richardson                  hamiltondestiny@gmail.com           Sports      Financial         1              101.67            101.67          PayPal    2025-01-15       Illinois            64   Other
    622  1a03d75b-8975-4098-bb90-d8c666de2819          Christian Kaufman                     davidkennedy@yahoo.com         Clothing     Government         3              287.23            861.69      Debit Card    2024-07-05           Ohio            54   Other
    623  17bfd447-935f-4f5e-89b3-5c7e17791a1f              Collin Norton                      leviaguilar@yahoo.com           Sports          Small         3              349.29           1047.87            Cash    2025-02-12           Ohio            20   Other
    624  3a3b66b1-8d1d-4374-b1a3-4212be49bb56              Patrick Baker                        tina68@robinson.com             Home          Often         2              483.74            967.48  Mobile Payment    2025-02-06     California            41   Other
    625  04dc57f9-cec5-453e-8278-f8adf0fcc5db                  John Ward                   jacksonwilliam@gmail.com             Home         Appear         5              287.75           1438.75  Mobile Payment    2024-08-21       New York            62  Female
    626  93fbd69c-ea82-49da-9b7b-eda93f631fc0                Cody Nguyen                    weaverdebra@hotmail.com           Beauty      Knowledge         5              164.97            824.85      Debit Card    2024-09-28     California            46   Other
    627  276a70f7-c371-465d-b547-31b22a5dd8dd              Alyssa Ibarra                 kimberlyromero@bennett.com         Clothing          Study         4              487.69           1950.76     Credit Card    2025-03-15     California            24  Female
    628  62f01b70-427b-48af-8c7b-33f95241ad17                Chad Garcia                   maryrasmussen@parker.com        Groceries          First         5              365.92           1829.60     Credit Card    2025-02-11        Georgia            55   Other
    629  4f8b4d6a-1bfc-4f1b-9697-435e57c616f8           Olivia Mcconnell                      youngdonna@mendez.com             Toys         School         1               90.44             90.44  Mobile Payment    2025-01-23        Florida            40    Male
    630  4333e8a5-eb27-474d-9228-12452eef9329                 Shawn Luna                  phillipsnyder@hotmail.com           Beauty           Kind         3              136.57            409.71      Debit Card    2025-01-09   Pennsylvania            63    Male
    631  ae07a2d9-9ae8-45e6-b99d-cced8e569e3d               Gail Herrera                          tracy39@yahoo.com      Electronics           Also         5              214.32           1071.60          PayPal    2024-05-18        Florida            19  Female
    632  2127937f-5561-42b4-80d0-34e13188a032                David Huber                  justinchambers@thomas.com           Beauty          Field         4              287.95           1151.80     Credit Card    2025-03-23           Ohio            38  Female
    633  237b1177-8767-4c56-bb15-dcbbf46bbb73                David Braun           obrienmargaret@turner-weaver.com             Toys           Fast         4              278.14           1112.56          PayPal    2024-08-24        Florida            46    Male
    634  ccb031ba-a132-4e4b-a8bc-c0dc3ce90a54              Bruce Herrera                         zsummers@gmail.com      Electronics           Town         2              283.27            566.54      Debit Card    2024-07-21   Pennsylvania            33    Male
    635  1190a50f-17df-4fb5-ba8c-a19a35ebc38f               Laura Kramer                       darren48@hotmail.com      Electronics       Everyone         4              310.82           1243.28          PayPal    2024-06-06        Georgia            65  Female
    636  7bdc2688-f3c5-4ef1-90e0-bef3d3b63427              Aaron Patrick                   catherinehughes@vang.com       Automotive           Main         3              249.03            747.09          PayPal    2024-10-08           Ohio            31  Female
    637  89e6dcdc-bad1-4cda-86d9-7decde90c061              Crystal Clark          stricklandtroy@peterson-allen.com       Automotive       Question         2              496.46            992.92          PayPal    2025-01-22           Ohio            51   Other
    638  83ab06c2-9d2b-4dfb-b8fc-2c4c096afb83              Jose Harrison                            lmills@ford.com           Beauty      Executive         2              464.44            928.88      Debit Card    2024-12-04       Illinois            20    Male
    639  bee952ff-7322-49a0-982f-c0238c39623a          Melinda Blair PhD                     poncedavid@hotmail.com       Automotive          Heart         4              149.21            596.84            Cash    2024-07-09       New York            30    Male
    640  019b18a9-fa0c-4a81-94aa-3b85b84119ba              James Simmons         wrightpatricia@thomas-richards.com           Beauty          Ready         1              119.14            119.14          PayPal    2024-05-02       New York            59   Other
    641  db5cc255-2ad9-4a41-8e6a-869298e2b229          William Blackwell                  stanleyedward@hotmail.com      Electronics         Effort         3              359.20           1077.60            Cash    2025-02-12          Texas            67   Other
    642  e2f59754-f229-48b1-8e4f-fc6e3b26f22f            Robert Guerrero              jessicasmith@hunter-ortiz.com           Beauty         Answer         2              245.83            491.66          PayPal    2024-10-31          Texas            22   Other
    643  340f6b20-1bff-4fb4-999e-f3732b4bcd8e       Mrs. Miranda Schultz                          jason12@yahoo.com           Sports             Mr         1                9.45              9.45     Credit Card    2024-08-14        Georgia            19  Female
    644  3a8ce7cd-8bda-4757-a3b7-3767bfaaca75            Benjamin Macias                       ijohnson@hotmail.com             Toys           Care         1              260.90            260.90            Cash    2024-05-08       Illinois            59    Male
    645  531db2d0-0bec-4419-9cf8-95c9c56da279                 Jose Blair                     tylerfleming@yahoo.com             Toys        Support         3               84.72            254.16      Debit Card    2024-12-17        Georgia            42  Female
    646  6704cacf-34a0-4515-a8e1-720106c1b8c5            Daniel Holloway                fgould@washington-brown.org           Beauty         Church         2              223.93            447.86          PayPal    2024-07-26     California            19    Male
    647  68507ce3-dea5-46db-9149-b6707dafad6b              Daniel Larson                  waltonandrea@reynolds.org             Home           Film         4              141.27            565.08     Credit Card    2024-11-02       New York            66   Other
    648  926c7dd6-89c1-4402-9522-30186913d2c9           Jordan Patterson                        ian86@townsend.info        Groceries         Writer         1              188.94            188.94      Debit Card    2025-04-20       New York            22   Other
    649  56e2de95-cb14-4457-a4af-5b5e65a1e19f            Morgan Sandoval                         taylor64@yahoo.com             Home           Care         3              336.53           1009.59  Mobile Payment    2025-04-04           Ohio            33   Other
    650  fa62d213-6c48-449e-9bc8-cd35417f4b7c              Michael Glenn                    ryandominguez@olson.org         Clothing       Election         3              269.28            807.84     Credit Card    2024-11-02       Illinois            49    Male
    651  7cda11b6-4c83-4312-90f0-91f468f3d58d               Joshua Price                      katherine29@yahoo.com             Home              I         1              425.12            425.12      Debit Card    2024-12-08       New York            67  Female
    652  c00536dc-e7fc-4c4e-9828-e2e14c12fc13             Elizabeth Hill                        ilawson@burnett.net             Toys          Space         5               20.70            103.50  Mobile Payment    2025-03-15   Pennsylvania            37  Female
    653  42b7fc1d-9b1b-4ea7-a824-188692030aa8               Rachel Jones                         travis00@gmail.com      Electronics           Fall         3               58.78            176.34      Debit Card    2024-10-14       New York            29  Female
    654  9217491f-8004-47ee-bdb5-6584c405e6ce            Mackenzie Burch                  howardtimothy@hotmail.com           Beauty         Likely         2              262.18            524.36  Mobile Payment    2024-08-03       New York            54  Female
    655  a4cb36d8-4131-49f0-8913-3907c4880411                Ryan Butler                            yreed@gmail.com      Electronics           Face         1              187.31            187.31            Cash    2025-01-16       New York            57  Female
    656  55666136-c664-405b-ab9a-dab96e1e241f                Kathy Hurst                     kathrynpoole@gmail.com         Clothing            Get         3              152.30            456.90     Credit Card    2024-06-01        Florida            54  Female
    657  116a22b2-7e6d-4b02-98bc-96283b374c8d              Mr. Eric Cruz                         ronald60@gmail.com      Electronics           From         5              375.44           1877.20      Debit Card    2025-02-09           Ohio            67   Other
    658  10ded973-cd3d-4220-97a7-a6a490258bf1              David Michael                  brookstara@walker-lin.com       Automotive            Off         4              222.58            890.32          PayPal    2025-04-17     California            34    Male
    659  ca6b5563-8459-4838-a6dd-471c40c77836               Phillip Webb                          david10@costa.org             Home          Whole         2              366.47            732.94      Debit Card    2025-02-24        Florida            19    Male
    660  2efdca9d-1b0f-4161-ba06-39e770e62b37                 Lisa Davis                      timothy79@roberts.com           Sports        Husband         1              126.88            126.88     Credit Card    2025-04-22          Texas            66   Other
    661  67844873-44f3-49d4-82cc-504842b7baf2             Michael Grimes                      alexander82@gmail.com      Electronics         Doctor         1               11.99             11.99          PayPal    2024-07-30       New York            27    Male
    662  c8b558b8-6875-407d-832b-a455ddd9b9d9            Kelsey Alvarado                          flawson@gmail.com         Clothing          While         3              215.27            645.81      Debit Card    2024-08-27        Georgia            58    Male
    663  855dd7bd-94d9-46ae-a803-1e222b4dfb7e            Kimberly Harris                        omarblake@gmail.com       Automotive            Our         4               34.61            138.44  Mobile Payment    2024-08-25        Georgia            51   Other
    664  7120e700-c4e5-47de-894c-aaacfdc8c3ac             Tiffany Mooney                        brownjose@gmail.com           Beauty         Effect         3              333.00            999.00  Mobile Payment    2025-03-06        Georgia            25    Male
    665  4d58d8d2-6208-441d-9885-4c520985fcc5                 Ashley Liu                         jeremy32@gmail.com       Automotive           Play         2              368.83            737.66     Credit Card    2025-04-29          Texas            31   Other
    666  5a71e05c-a4e7-41a9-8d60-102c258c16ed              Kevin Johnson                            mrich@gmail.com      Electronics         Degree         2              253.75            507.50      Debit Card    2025-04-17        Florida            44  Female
    667  58bdf523-5777-4d6c-ac1a-219283b38d5a            Brittany Phelps                 adamslance@pena-brooks.com             Home      Represent         3               28.79             86.37            Cash    2024-11-03   Pennsylvania            67   Other
    668  745a93c7-5c50-44e9-b95b-7a07bd357661                Jack Wilson                     amberpittman@yahoo.com      Electronics          North         2              308.42            616.84     Credit Card    2025-02-17       Illinois            62  Female
    669  d1cc686e-d628-41f7-97af-afeef3e52d39              Mary Guerrero                     johnsonmike@davies.com         Clothing         Animal         1               62.25             62.25     Credit Card    2024-12-17       New York            46   Other
    670  a23e702d-5c1c-4569-8608-68660e65970a                Nathan Tran                   matthewjohnson@white.com        Groceries          Tough         5              346.92           1734.60     Credit Card    2025-04-28     California            31    Male
    671  d909918e-ade7-4fb9-860d-ec0649e3c7e8            Brittany Miller                      lrobinson@harris.info           Beauty             Do         4              354.39           1417.56  Mobile Payment    2025-02-03     California            42   Other
    672  5dbc596e-b044-4cb9-bf63-7cae72ec83df        Ronald Williams Jr.                          jesus99@floyd.com           Beauty          Court         2              256.50            513.00      Debit Card    2024-06-08     California            49  Female
    673  fd79d8f1-636a-4f72-8bcd-f2b2079880c8              Julie Russell                     ericporter@hotmail.com             Toys     Difference         3              303.87            911.61      Debit Card    2025-01-26       New York            58    Male
    674  171e430f-e27a-4899-bb72-6ea19368ab52                 Debbie Gay               amandabennett@strickland.com           Sports        Believe         3              383.02           1149.06      Debit Card    2024-06-19     California            53    Male
    675  4c16f689-ea8d-4827-9043-6c93b569a64e               Linda Spears                         tweber@hotmail.com             Home             No         5              494.64           2473.20     Credit Card    2025-02-04          Texas            24  Female
    676  5a1ece2f-5870-4fa4-a42b-0ca42dde7122                James Olson                          unelson@yahoo.com       Automotive             He         4              180.64            722.56          PayPal    2025-02-20           Ohio            62   Other
    677  d9daa25b-e354-49d7-81f9-e993a840ee8b               Kerri Miller                         gstevens@yahoo.com       Automotive     Population         2              375.91            751.82  Mobile Payment    2024-05-04       New York            62  Female
    678  3f2aa4d6-d5a2-4856-a1e5-d3e163922f8b                Sean Knight                            kgreen@chan.net         Clothing            Box         2              322.29            644.58     Credit Card    2024-12-04   Pennsylvania            50   Other
    679  4723e2a6-3fd3-4ae4-985d-79c1919f7580               Misty Krause         sullivanpatricia@mcdaniel-shaw.org      Electronics          Truth         3               83.85            251.55      Debit Card    2025-01-06   Pennsylvania            43   Other
    680  5b0090e2-3390-47a0-838e-6b6f9668e07e             Jerome Fischer                          casey42@gmail.com      Electronics          Agent         4              251.32           1005.28      Debit Card    2024-10-05          Texas            32  Female
    681  d44d5053-83bb-4311-a98a-f559531cbcea         Christopher Miller                    matthew96@ho-chase.info           Sports        Despite         3              397.13           1191.39  Mobile Payment    2024-12-30        Florida            33   Other
    682  d472f6a2-edd7-4597-a31a-350816413808            Charles Griffin                          emily31@kelly.com             Toys           Fish         2              365.75            731.50  Mobile Payment    2024-05-19          Texas            39    Male
    683  9c137c5b-046d-46a5-b2f7-45223c9bc500            William Farrell                        robertgross@orr.org             Home          South         2               25.24             50.48     Credit Card    2024-07-15          Texas            59  Female
    684  721df553-ed45-4890-845b-4d6daca12c22                 Kim Orozco               nicole57@thompson-moreno.net      Electronics        Address         3              481.38           1444.14      Debit Card    2024-10-04          Texas            42  Female
    685  b28ba1a7-1260-47ec-a8f8-af1a746982f5                 Bruce Shaw                richardsonwilliam@yahoo.com      Electronics           Late         3              179.23            537.69     Credit Card    2024-11-24           Ohio            58   Other
    686  28aa2d4a-7d1c-430e-9be9-3d818209865e                Kevin Haley                  scottrodriguez@wilson.com         Clothing           Fact         4              225.18            900.72          PayPal    2024-06-24        Florida            65   Other
    687  7ab390b4-390f-406b-99dd-8bb175ebb8a3            Megan Donaldson                  xmiller@martinez-hunt.biz           Sports        Believe         2              492.13            984.26          PayPal    2024-05-15       Illinois            51    Male
    688  81b09aa6-20ea-48cb-8742-8bd3ad01348e                Mark Bryant                          jerry17@david.com      Electronics         Common         5              216.19           1080.95            Cash    2024-06-24          Texas            27    Male
    689  1047ed47-40f3-420b-9f88-08d89ddc4884            Elizabeth Boone                        candice66@brown.com             Toys          Thing         5              128.03            640.15  Mobile Payment    2024-12-26        Florida            38   Other
    690  b6e9fa17-cc5c-4b89-8bff-5bb79f78b0e5               Scott Mathis               ikennedy@welch-figueroa.info             Toys        Whether         3              440.55           1321.65      Debit Card    2025-04-17     California            25    Male
    691  5eac597c-07ed-4bb3-8d8f-62505d1d7aa7            Gregory Sanchez                        kenneth91@gmail.com           Beauty         Source         1              214.15            214.15          PayPal    2024-11-13        Georgia            64  Female
    692  4d573a9a-1e67-4603-956d-39e111360c5f             Alexandra Cook                   kennedyjoshua@foster.com             Toys        Science         1              368.91            368.91     Credit Card    2024-06-26        Georgia            31    Male
    693  20c27b07-ba77-4dd7-8fc6-38c5c038e4f4            Joseph King DDS                          susan66@gmail.com             Home          Blood         4              172.53            690.12     Credit Card    2024-08-11        Georgia            39   Other
    694  44a65709-02b5-4f6a-ba00-df0bb1f6e7c3                Johnny Cruz                        joneslori@yahoo.com      Electronics           From         4              264.46           1057.84  Mobile Payment    2024-09-29        Georgia            43   Other
    695  868fba44-cf10-429a-9605-71f4a11ac5ab                 Gary Horne                       kristen16@brown.info         Clothing      Recognize         5              205.43           1027.15          PayPal    2025-04-14        Florida            35    Male
    696  7e579b0b-18d3-486b-8519-ee4b898e3749           Michael Anderson                 raymondwalker@alvarado.org             Home        Clearly         3               90.75            272.25      Debit Card    2024-07-03           Ohio            18    Male
    697  fd4f5608-045f-45a9-a76f-53ee6422ae5d               Donald Lopez                      michele13@hartman.org             Home        Against         2              462.83            925.66            Cash    2025-04-02       Illinois            31   Other
    698  a36c4f82-7b78-45e3-ac57-7a1d8be25e5c               Jason Garcia                        brandon55@olson.com             Toys             On         2              175.68            351.36  Mobile Payment    2024-07-08     California            45    Male
    699  b924b3a0-f021-4f9a-a4fa-8e9977e54433               Julian Smith                        melissa62@duffy.com         Clothing        Nothing         3              158.05            474.15  Mobile Payment    2025-02-24       New York            34   Other
    700  cad73946-4c11-465b-95e7-c71d02106869                 Kevin Owen                          regina31@page.biz           Sports          Admit         4              171.25            685.00            Cash    2024-09-22       Illinois            61    Male
    701  3430d3fa-c1c0-4015-b329-6dbd1594c8a9               Amanda Patel                      gravesdavid@yahoo.com             Home           Have         1               55.93             55.93      Debit Card    2024-06-26   Pennsylvania            48  Female
    702  8bed04c7-19ce-4f67-b016-a84ac91fd65c               Anthony Good                 jessicalambert@hotmail.com         Clothing      Scientist         5               90.76            453.80          PayPal    2025-02-06       Illinois            19   Other
    703  a453ac80-dd6a-4372-a1f5-ce62f849c13f              Matthew Brown               parkergina@nguyen-parker.com             Toys          Today         1              466.10            466.10     Credit Card    2025-01-07          Texas            43   Other
    704  1befc387-54bf-432b-83a6-d74afa5a8c89             Linda Townsend                        santosdean@ruiz.com      Electronics        Partner         5               41.93            209.65     Credit Card    2024-05-06          Texas            52  Female
    705  f64d5e64-843e-49ce-85c1-e154a7d9b81b       Mr. Rick Crawford MD                          pmartinez@cox.com       Automotive            Bag         1              429.44            429.44            Cash    2025-03-28           Ohio            48    Male
    706  83b9140d-2627-4a2e-95f9-2a94e8dd0140        Jacqueline Williams                    huntandrew@sweeney.info         Clothing           Same         3               14.14             42.42     Credit Card    2024-07-06       Illinois            35  Female
    707  d0cf8f47-408c-41cc-a272-996ec8a8fdd7               Ryan Patrick                    carsonkevin@hotmail.com         Clothing            Ask         5              142.90            714.50          PayPal    2024-08-13       New York            38  Female
    708  b40d8cfc-db9c-4b8a-8081-e2604c5150bb           Kimberly Pearson                      morankelsey@smith.com           Sports          Adult         2              283.46            566.92          PayPal    2024-09-28        Florida            70    Male
    709  160df36d-0c17-4b12-bffa-85b7b75f7c5b              James Hawkins                           adoyle@gmail.com        Groceries           Side         4              372.25           1489.00      Debit Card    2025-04-08       New York            34   Other
    710  35dc292b-8d1d-4d77-992f-4855aaa70550             Jonathan Hodge                         karen99@patton.com           Sports       Economic         5              375.98           1879.90            Cash    2024-06-20        Georgia            56  Female
    711  0f3ad2fc-0717-4127-a632-b3b29d101618                David James                 blackwellmaria@hotmail.com         Clothing         Strong         1              134.85            134.85          PayPal    2024-10-11       Illinois            21    Male
    712  e809b00c-8ef8-486b-a1be-3e0f10564512              Lydia Jackson                 katrinafischer@hotmail.com           Sports           Dark         2              296.19            592.38            Cash    2024-11-18       New York            21  Female
    713  9124b9ce-72fd-49a7-975e-e10ee63e3eba                Debra Davis                           ryan76@yahoo.com             Home         Accept         1              351.05            351.05  Mobile Payment    2024-07-25           Ohio            28   Other
    714  c3fb0148-d170-49c2-b2f7-d6f24a74f20e             Tanner Santana                      qshelton@franklin.com      Electronics           Show         4              277.89           1111.56            Cash    2024-07-25          Texas            66  Female
    715  bdebe2fb-92a0-418b-8d8a-01d3ec0bed84                Renee Glenn                     hugheshailey@moore.org        Groceries             Us         5              460.25           2301.25          PayPal    2024-10-08          Texas            32  Female
    716  e348e16e-854d-42d8-8966-e28882f398bc              Ryan Franklin                   flong@bailey-johnson.biz             Toys           Able         1               95.60             95.60      Debit Card    2025-04-08       New York            36    Male
    717  65b19c06-1eb4-4060-9af5-ba88dcfd1457               Jamie Warren                     donnadickson@watts.com             Toys       Whatever         2              404.76            809.52          PayPal    2024-09-27   Pennsylvania            40   Other
    718  e7daf93e-e98f-4f98-bd95-e5bdf51db727            Elizabeth Myers                   trevorthompson@smith.com           Sports            Air         2               40.22             80.44  Mobile Payment    2024-06-29       New York            20   Other
    719  da8b4718-d0ea-4b54-bc86-be4c0ec2b864                Ryan Taylor                         ojohnson@cooke.com         Clothing         Couple         4              432.57           1730.28      Debit Card    2024-11-16       Illinois            51    Male
    720  7e7ac609-fb27-4044-b17a-87cb3336f4f6             Lonnie Pearson                     john60@blair-huber.biz           Beauty     Throughout         4              470.92           1883.68     Credit Card    2024-10-15       Illinois            59    Male
    721  b4e316fb-bd27-4908-9db3-0aa6b8020764                 Latoya Cox                         tony21@hotmail.com           Beauty       Remember         4               12.68             50.72      Debit Card    2024-08-05   Pennsylvania            40   Other
    722  d78d9c78-4861-4962-bbee-2a21016148a2               Raymond Hunt                     brooksgloria@garza.com         Clothing        Country         4              451.86           1807.44            Cash    2024-09-24        Florida            64  Female
    723  2ef54031-a687-4ee5-949c-f94694adb1b8                Amanda Peck                       heather83@benson.com           Sports       Audience         4               84.46            337.84          PayPal    2024-07-31        Florida            19   Other
    724  16ff9714-2ea7-4517-8194-c78b6bef4d0c                Jason Brown                   jonesmatthew@hotmail.com        Groceries         Father         3              441.64           1324.92  Mobile Payment    2024-05-17          Texas            41   Other
    725  8d82f902-8ade-46d6-a144-b7786d37e483           Alison Rodriguez                          karen23@gmail.com         Clothing           Tree         2              404.90            809.80          PayPal    2024-11-30        Georgia            46  Female
    726  5288f0e3-546b-4769-bb87-f8150a06af3a              Victor Martin                        helen00@hotmail.com           Beauty          Teach         1              255.86            255.86      Debit Card    2024-10-15           Ohio            58   Other
    727  23361391-f481-4b4f-976c-369c07b20d78            Patrick Preston                      heather94@swanson.com       Automotive         School         1               25.53             25.53            Cash    2024-06-06       New York            62  Female
    728  f1209f45-6eea-468f-826d-39f4d6959671                Molly Adams                     johnalvarado@white.org       Automotive     Successful         1              120.40            120.40  Mobile Payment    2024-06-25           Ohio            70    Male
    729  bfd31efd-9201-434a-8d16-a2c672ec6003              Daniel Wilson                   kelly47@strong-bowen.org           Beauty          First         2              231.30            462.60            Cash    2025-03-27           Ohio            32  Female
    730  faba26a0-f81f-4441-8e5d-111277a83693               Bruce Nelson                            ytran@gmail.com      Electronics          Along         1               13.16             13.16  Mobile Payment    2024-12-28       Illinois            45    Male
    731  2a4eb04b-5e37-45ca-888b-c1b6cda79eaa              Michael Lopez                  yodermichelle@miller.info           Beauty        Western         5              366.68           1833.40  Mobile Payment    2024-12-12          Texas            22   Other
    732  e9b28e1e-a182-4b66-986e-823f3ca1cfe8               Adam Spencer                bcollins@martinez-boyer.org             Toys             So         4              400.82           1603.28      Debit Card    2025-01-09        Florida            41    Male
    733  1d9a7f77-2ec3-4fc9-bf68-a0ddcbef3cb8          Miss Laura Graves                        tstewart@young.info         Clothing          Trial         1              394.27            394.27      Debit Card    2024-12-10   Pennsylvania            55    Male
    734  8c0bc906-1ef5-43dd-b595-78546ecec307              Robin Richard                           fsalas@yahoo.com         Clothing            But         4              261.04           1044.16      Debit Card    2024-05-07           Ohio            57  Female
    735  d14118f4-cec8-4632-ac1f-5cb7d1906431              Shawn Murillo                           bmoss@atkins.com           Beauty          Third         4              354.33           1417.32          PayPal    2025-01-28          Texas            40   Other
    736  43c30ee5-d863-4d92-9993-d0f41dcf380c              Alvin Salazar                   snyderkendra@hotmail.com        Groceries           Size         4               18.96             75.84            Cash    2024-07-26           Ohio            64   Other
    737  2a1209a5-bf77-4953-9824-f3d46fbac023          Jonathan Anderson                        ngonzalez@munoz.com        Groceries         Decade         1              278.29            278.29            Cash    2025-04-18           Ohio            52    Male
    738  08ab78b6-27f8-4aa0-b6a2-87d1d31c9ebf           Deborah Santiago                 zrussell@jones-hickman.com         Clothing           Team         3              177.57            532.71            Cash    2024-09-24           Ohio            39    Male
    739  6d41e77b-ceb5-482a-a394-4bc8ccff9707            Cynthia Woodard                   williamssara@jackson.biz           Beauty          Guess         1              143.88            143.88  Mobile Payment    2024-05-11       New York            43  Female
    740  cb7bb584-8c28-436e-b690-2f173bd621ad                Lisa Walker                       eferguson@garcia.com         Clothing           Lead         3              269.62            808.86     Credit Card    2025-04-23     California            53   Other
    741  028421ee-89d5-4ad0-9405-6056656c74b3             Sabrina Levine                     alyssaingram@ramos.com      Electronics        Economy         1              463.52            463.52      Debit Card    2025-01-10     California            45   Other
    742  054279dc-8f3f-411f-934c-c0541ba4df64                 Henry Hall                   reedcharlotte@weaver.com         Clothing         Accept         3               92.17            276.51            Cash    2024-11-19           Ohio            36    Male
    743  4e7705d2-0434-408c-be2b-8bb335d199d3              Charles Reyes                       eparsons@hotmail.com           Sports         Senior         1              298.18            298.18      Debit Card    2024-08-21          Texas            32    Male
    744  51a264a6-8370-49ad-9237-dde1f2af1f1e              Deborah Baker                      sharpconnie@gmail.com      Electronics           Play         2              113.90            227.80      Debit Card    2024-09-18       Illinois            19    Male
    745  c3c1a290-e471-4a7e-9b30-1122864aaf07               Amanda Evans                         lisa75@sampson.org           Beauty       Democrat         1               57.61             57.61  Mobile Payment    2025-04-22       New York            53    Male
    746  44270e1e-b7a0-44ff-927d-42019cba9999           Stephen Williams           johnathanwalters@acosta-wise.com      Electronics       Building         5              160.08            800.40  Mobile Payment    2024-05-17        Georgia            28   Other
    747  7d3eee0b-2860-4723-ae04-0ee237bccaf1              Robert Butler                        xwilliams@yahoo.com         Clothing           Nice         4              149.26            597.04          PayPal    2024-09-19        Florida            63  Female
    748  c548881e-8b17-45db-b91b-62a482e05bce                 Lisa Smith                     boonejeffrey@yahoo.com             Home            But         2              414.12            828.24      Debit Card    2025-01-20       New York            20  Female
    749  2ac244b3-64aa-4819-9909-bec302fcaeb2               Amanda Ponce                     jcontreras@delgado.com        Groceries             We         1              470.72            470.72     Credit Card    2024-10-04        Georgia            41  Female
    750  28ddbc12-dc3c-4e05-b68f-da8122e42e08                Howard Sims                      spencerleah@gmail.com           Sports           Thus         5              456.82           2284.10      Debit Card    2024-11-12          Texas            23   Other
    751  780260e7-9ccf-41dd-a829-e43d2abc3863                John Campos                      shelbymaddox@reed.org             Toys            May         5              176.00            880.00  Mobile Payment    2024-09-19       New York            46    Male
    752  62bbb0bf-8633-4f68-9d53-b69af27cbc9f              Patrick Weeks                         larry72@moreno.org        Groceries       Training         4              181.37            725.48  Mobile Payment    2024-10-11       New York            69    Male
    753  80d67ae0-6609-474d-a005-cafcb9b8f1c8           Jacqueline Allen                            pperez@neal.com       Automotive        Picture         3               46.99            140.97      Debit Card    2024-06-14          Texas            45    Male
    754  59bad113-a15f-4c0e-a42e-9bfb53186605                Mariah Lutz                  claytonwilliams@gmail.com             Home        Evening         4              222.81            891.24          PayPal    2024-05-12           Ohio            45   Other
    755  d04aaa0d-40cb-4713-92fb-8c8c403e7018             Theresa Romero       millermatthew@alexander-phillips.biz       Automotive     Collection         5              454.54           2272.70      Debit Card    2025-02-03           Ohio            59  Female
    756  8f974e94-4d07-45a5-b84f-93380b39260b             Ricardo Wilson                    ashleyedwards@lopez.com           Sports        Science         5               28.27            141.35            Cash    2025-04-27           Ohio            45   Other
    757  76bc649f-9afa-4344-8ead-9566cef12a79            Victoria Chavez                            jrice@gmail.com       Automotive           Fast         2              411.88            823.76      Debit Card    2024-06-27     California            53    Male
    758  0276f356-9d78-46cf-a476-1b474815ca0d              Ashley Hooper                     timothyhill@rivera.biz       Automotive            But         1               96.88             96.88          PayPal    2024-09-18   Pennsylvania            41  Female
    759  fdc15073-b6d0-451f-9fbe-2ebdb1eb9763              Angela Miller                          renee71@gmail.com         Clothing          Total         5              415.07           2075.35      Debit Card    2024-11-02   Pennsylvania            58  Female
    760  42523a59-2be6-4d56-888f-88d9bcaa0a53            Robert Robinson                    matthewsmith@garcia.com             Toys       Discover         5              133.14            665.70     Credit Card    2024-08-24   Pennsylvania            33    Male
    761  51923a47-62ab-4fcf-8d1d-1da01fcf699c              Eric Martinez              johnjohnson@baker-edwards.com           Sports           Read         2              395.45            790.90  Mobile Payment    2024-11-26        Florida            26    Male
    762  c5617829-a4d1-4a1d-bfa9-f8493b93046f               Noah Padilla                        uwilson@hotmail.com       Automotive            The         1              261.28            261.28     Credit Card    2024-12-29   Pennsylvania            18  Female
    763  4bc4a53c-4ea7-4a4d-b2c5-d22a548b5e4f                Gary Hanson                   williamcoleman@allen.biz           Sports           Rock         2              378.60            757.20      Debit Card    2024-10-29        Florida            24   Other
    764  1bba69f5-e0c2-4aba-99f6-806ba16ac364      Christopher Blackwell            jenkinsbrett@watson-russell.com         Clothing           Bill         1              206.32            206.32      Debit Card    2025-04-08          Texas            52  Female
    765  922e6abd-8782-4de9-a8c7-1dc7724f8278            Kathy Velasquez                           achang@gmail.com           Beauty          Whole         4              398.63           1594.52          PayPal    2025-03-23        Florida            25   Other
    766  1239b644-640d-4f36-ac4e-9059cf3a7689                  Dale Knox                    hancockjasmin@moore.org             Toys            Arm         3               22.00             66.00          PayPal    2024-11-22     California            60  Female
    767  7351e6fa-6b4b-48fd-8bc0-0c7bda2d906d            Sarah Henderson             andrewyoung@cooper-marquez.net             Home         Result         1              205.96            205.96      Debit Card    2025-02-08          Texas            51    Male
    768  0ef6a672-b41a-4e33-8e6f-21bab8101be5            Corey Zimmerman                     phelpsjulie@thomas.biz        Groceries           Door         1              153.19            153.19     Credit Card    2024-05-07   Pennsylvania            67    Male
    769  7a6375ca-32e3-4fba-81a8-c2e0b2558223                Mark Lucero                  marshallmolly@patrick.com        Groceries            Let         1              419.81            419.81      Debit Card    2024-09-25     California            69  Female
    770  584de303-ad55-4b1b-9401-e3973a57ca26                Holly Smith                     tanyamorrow@floyd.info           Beauty          Claim         4              193.84            775.36            Cash    2025-01-15     California            24  Female
    771  381c1001-a2fc-4f29-b473-8801498c692d            Edwin Patterson             lesliebowman@gonzalez-wade.biz             Home          Every         3              330.96            992.88          PayPal    2024-10-26        Georgia            35    Male
    772  a53ba032-0c57-44cc-9bf9-8f5170a8bf76           Richard Thompson                      reyescarl@perkins.com       Automotive          Staff         2               84.23            168.46      Debit Card    2024-06-08   Pennsylvania            23    Male
    773  3face476-4f84-4835-97a3-5e02332eb757            Elizabeth White                        patricia60@cook.com        Groceries           Term         1              477.87            477.87  Mobile Payment    2024-07-11          Texas            28  Female
    774  a7f56cc5-ef88-42df-a381-186ba07b7638             Christy Taylor                    dakotasmith@hotmail.com             Toys   Particularly         1               83.14             83.14          PayPal    2025-01-14       Illinois            43  Female
    775  9e5b1cac-7046-471e-999f-2250505b89c2                  Jacob Fox                  stephenjohnson@miller.com           Beauty        Partner         4               98.73            394.92     Credit Card    2024-09-15           Ohio            50    Male
    776  7afbf306-fb65-49e7-932e-c7b8d8d4cab7            Alexander Jones                        david27@hotmail.com             Toys          Enjoy         3              193.34            580.02      Debit Card    2024-07-31       New York            64    Male
    777  25945156-83cf-4931-a296-f347ed09b928           Joshua Rodriguez                    harveydaniel@abbott.com             Toys          Third         2              103.98            207.96  Mobile Payment    2024-10-29           Ohio            42  Female
    778  67f78ea7-943e-42e1-802b-6b20b60b6bd9                 Keith Wood                   holmescynthia@baxter.com       Automotive          Apply         4               54.00            216.00  Mobile Payment    2024-06-24           Ohio            32   Other
    779  03986f17-0445-4d17-b474-7be3b67e6f85            Heather Benitez                      kimberly11@ortega.com             Toys            Yes         2               14.57             29.14  Mobile Payment    2025-02-18        Georgia            62  Female
    780  5f05908d-ad27-491a-83f2-7628c404bb94          Angela Montgomery                      steven35@mccarthy.com       Automotive          Small         1              155.14            155.14     Credit Card    2024-10-31     California            63    Male
    781  d99d90ec-0cf0-4b70-b31b-15b63f514daa                David Hicks                      austinmoore@gmail.com        Groceries        Culture         3               44.72            134.16            Cash    2025-03-09          Texas            30   Other
    782  6dc79a26-7c10-419e-9653-3cc85b81ecfb               Carla Hanson                       smallemily@gmail.com        Groceries         Itself         1              477.68            477.68            Cash    2024-12-08        Georgia            59    Male
    783  01d191e3-1529-4194-834c-a4e9cfc67bb4           Maria Fitzgerald                    deborah71@davenport.biz       Automotive         Theory         1              326.19            326.19          PayPal    2024-08-03        Florida            55   Other
    784  c9eef06b-3b7f-4565-acad-c055c3275f74            Priscilla Brown                garrettrichardson@gmail.com       Automotive          Exist         3              376.70           1130.10          PayPal    2024-11-14        Georgia            58    Male
    785  d9da774e-1647-49d8-b998-fbe8ebd2b426                Lauren Wolf                       olsonfaith@yahoo.com             Toys        Century         4              105.67            422.68          PayPal    2024-07-17           Ohio            22    Male
    786  6786d105-8ae0-47c5-8711-01cc51638f7c      Dr. Charles Torres MD                 jeremywelch@hernandez.info             Home           That         1              268.51            268.51     Credit Card    2024-11-19   Pennsylvania            63    Male
    787  eada0014-3888-43c9-bef9-141f444c3f1a               Maria Franco                       michael88@gordon.net       Automotive          Which         1               30.55             30.55  Mobile Payment    2024-06-17       Illinois            57    Male
    788  1f2c3c7f-a6a5-4623-97b6-4d5c545934e1                Johnny Diaz                   beckjeremiah@hotmail.com           Sports       Hospital         2               96.54            193.08            Cash    2025-02-18       New York            63   Other
    789  124504ac-dead-474d-83d2-34f5f59175ff       Kimberly Martinez MD                    mattheworr@sullivan.com         Clothing         Matter         5               56.62            283.10      Debit Card    2024-05-31        Florida            25   Other
    790  ebac1865-1720-4c5b-9804-45f23dff3488             Barbara Durham                  fernandomiller@murray.com       Automotive           Poor         3              470.74           1412.22            Cash    2024-10-16          Texas            25    Male
    791  5e2ca272-5924-4171-81d8-09b725ed5f96              Megan Alvarez                   hughesmorgan@nielsen.net       Automotive            Top         1              275.36            275.36  Mobile Payment    2024-10-17       New York            24  Female
    792  949630f8-0767-49cb-90b5-65e4aa25109c              Katelyn Smith              michelle35@massey-collins.org        Groceries      Authority         2               26.52             53.04      Debit Card    2025-04-20          Texas            27   Other
    793  9d99d407-dfa3-4fef-b0c5-8a45baa17a95              Michael Moore                          debrapark@lee.com         Clothing             So         2              310.30            620.60          PayPal    2024-06-26        Georgia            46    Male
    794  63155f27-a64f-41a6-8ceb-89e5390ece67             Michael Moreno                 williamsandrew@hotmail.com      Electronics          Chair         2              306.63            613.26      Debit Card    2024-07-23        Florida            45  Female
    795  7da74804-0c4b-4325-b7e1-8c126e056aec              Courtney Hall                       jeffery57@thomas.com      Electronics          Place         5              131.56            657.80      Debit Card    2024-12-08        Florida            43  Female
    796  271348d4-8ff0-4739-bcf3-a63ac5bd919c            Alyssa Fletcher                        michael85@cantu.com           Sports           Five         1              177.08            177.08  Mobile Payment    2024-08-10          Texas            43    Male
    797  783c3414-ff9d-427c-a596-01f31a9aebd8            Roberta Collins                      martinjames@myers.com         Clothing     Production         2              413.60            827.20  Mobile Payment    2024-08-11           Ohio            56  Female
    798  d9238c22-50fc-4ac4-8522-52796eb5dc44               Paula Carney                          karen79@gmail.com        Groceries         Recent         4              240.71            962.84          PayPal    2024-08-18          Texas            54  Female
    799  47d1b25c-fc1a-4912-81ad-2b97e83ed102               Nathan Stark                dbrown@williams-mullins.net           Beauty          Space         5              336.23           1681.15            Cash    2025-01-25        Georgia            51   Other
    800  1de67094-d8dd-4806-85fe-c727940a4e7e            Jasmine Stewart                      davidgolden@gmail.com           Sports           Join         2               57.97            115.94      Debit Card    2025-03-12       Illinois            30  Female
    801  0c82f906-4fc6-40bd-8dde-d9f7809950b8                 Mark Myers                   ygarrett@howell-wood.com        Groceries           Send         2              171.90            343.80            Cash    2024-12-25           Ohio            27    Male
    802  2fcd6c44-8232-4aeb-b21e-56bb99d17c8f                Jessica Lee                         michael63@ruiz.com       Automotive     Throughout         4               45.77            183.08      Debit Card    2024-12-10          Texas            55  Female
    803  bd31d81d-9ae5-425c-a586-1c4f102e7e4d               Andrew Klein                         mary51@sanchez.biz           Sports        Account         2              412.09            824.18      Debit Card    2024-11-16       New York            31  Female
    804  8df06cf8-a39c-410c-8a7b-85556a19594d              Thomas Little                         zmcmahon@yahoo.com             Home        Foreign         4              415.41           1661.64            Cash    2024-10-01           Ohio            58   Other
    805  7e1ea192-f60d-4d50-9f4e-524dee561e44                Joseph Ross                      erikawatson@perez.com           Sports          Group         3              492.85           1478.55      Debit Card    2024-09-12           Ohio            63  Female
    806  670394e9-8f29-4b4c-822a-f236abb6864f                Megan White                    melissa74@rodriguez.biz        Groceries       Marriage         3              412.99           1238.97     Credit Card    2025-01-09        Florida            31  Female
    807  b3520c53-eb95-4ec9-bab1-8b3f5defcabd                  Jack Frey                         ibrown@hotmail.com         Clothing       Official         1               19.63             19.63          PayPal    2024-07-29          Texas            18   Other
    808  cb60f885-0225-4840-bcaa-ea15c76dbd59           Melissa Hamilton                     james61@clark-diaz.biz         Clothing        Trouble         4              482.37           1929.48     Credit Card    2024-12-10           Ohio            60    Male
    809  f1eb59fb-8f6e-4192-8024-ea9d75208c01             Andrea Vaughan                      fosterdavid@yahoo.com       Automotive          Cause         4              143.04            572.16     Credit Card    2025-04-17       New York            68   Other
    810  6397c936-2233-4014-8e72-2f646d7a89de               Ashlee Brown                  gibsonelizabeth@yahoo.com         Clothing            Nor         3              169.18            507.54     Credit Card    2025-03-22        Georgia            43    Male
    811  cc8f28f8-9fb2-42ad-b1d8-c1f1e5755ecc               Holly Miller                       lwhitehead@yahoo.com             Home        Section         2              480.55            961.10     Credit Card    2024-12-09          Texas            25   Other
    812  0b3a972b-3e30-4264-9499-ca66884c0a87            Jerry Rodriguez                       donnaclark@stark.com       Automotive           Yeah         2              100.61            201.22     Credit Card    2024-11-13   Pennsylvania            39    Male
    813  73fdaec6-c29a-46a3-8ca2-06894fff325e                 Jorge Kane                          wbowers@neal.info           Beauty             No         2              282.87            565.74      Debit Card    2025-02-26     California            48  Female
    814  da22ae0a-d660-430a-b092-dde07950f536             Stephanie Diaz               brennanvalerie@zimmerman.com           Sports         Worker         3              405.47           1216.41     Credit Card    2024-09-06       New York            30    Male
    815  c9ce0624-6a60-43a6-b927-4acf2a62a757           Matthew Thompson              katherine40@adams-edwards.com             Home           Than         3              377.80           1133.40      Debit Card    2024-06-14        Florida            58    Male
    816  1a06c317-f550-4f0f-b638-633d677472bc                 John Moore                        gilljason@gmail.com        Groceries           Pass         3              236.93            710.79      Debit Card    2024-06-11           Ohio            21  Female
    817  3560ada0-2a6b-4957-b59a-c3f4450a624c              Curtis Fuller                       christina22@barr.com      Electronics           Unit         2               13.58             27.16  Mobile Payment    2024-12-22        Florida            69  Female
    818  aab344f8-4160-4b38-98a3-ac7df34dcdbb           Dr. Edward Lewis                  parrishmelissa@parker.com       Automotive         Though         1               33.78             33.78  Mobile Payment    2025-03-23           Ohio            57   Other
    819  82bff564-558f-4fe7-81a9-be8feb607fea              Kelly Spencer            hernandezchristopher@barker.com             Home   Organization         5               59.61            298.05          PayPal    2025-04-13        Florida            36   Other
    820  e9a30704-bff9-40de-952b-7354d724aaed                 Jaime Ross                        cindycruz@yahoo.com           Beauty           Deep         2              347.19            694.38            Cash    2025-01-10        Florida            37    Male
    821  11faf4d2-3082-42b0-a52e-750745f21e93                  Jacob Cox                           zvilla@miles.com        Groceries          Woman         1               48.40             48.40      Debit Card    2024-08-28        Georgia            70  Female
    822  b734d3d1-a916-4f13-bbc0-bff80ce59d3c              Joel Thompson                        fguerra@hotmail.com             Home           Vote         3              449.67           1349.01  Mobile Payment    2024-06-09          Texas            43  Female
    823  8b3bb4f7-845e-435b-8118-e66ba3fcb3ff             Rebecca Steele                          bpage@hotmail.com         Clothing           Safe         3              317.85            953.55  Mobile Payment    2025-04-23       Illinois            24   Other
    824  6edad6b7-40fa-4938-86e1-aa609de98799            Brendan Sweeney                hansonnathan@clark-reed.org         Clothing          Party         2               79.56            159.12      Debit Card    2024-08-13       Illinois            49   Other
    825  4ab4a7db-df88-4c2a-aaa4-33abed03f523                Dalton Hill                      fcampbell@hotmail.com       Automotive          Heavy         1              330.84            330.84          PayPal    2024-12-21   Pennsylvania            44  Female
    826  6a2a50f1-6d9e-44e4-9a84-25146b878599           Leonard Friedman                       latoya39@wilson.info           Sports    Environment         3              473.00           1419.00            Cash    2025-04-07        Georgia            23  Female
    827  8ad14f48-fd4f-4dec-ac06-c12fa983863c               Charles Hill                           ohardy@yahoo.com           Beauty        Country         5              362.40           1812.00  Mobile Payment    2024-09-20       New York            37    Male
    828  5605bfca-c0c8-4974-b6c6-da73f780b98f                 Carl Price                     juanbrown@sullivan.com      Electronics          About         1              303.92            303.92      Debit Card    2024-11-10       New York            35    Male
    829  a61f6096-5849-4030-9a52-429971376582         Mrs. Anna Olson MD                         yalvarez@moore.com        Groceries        Section         4              288.20           1152.80     Credit Card    2024-10-21   Pennsylvania            61    Male
    830  0be8dc56-0014-4db5-b870-b40b219776f1          Matthew Henderson                            wmayer@diaz.com        Groceries         Action         1              410.23            410.23          PayPal    2025-04-17           Ohio            64    Male
    831  baac6e5c-d7e0-464f-b748-51e47652899e                 Cody Lloyd                     brookefarmer@yahoo.com      Electronics         Wonder         4               92.87            371.48      Debit Card    2024-10-21     California            51    Male
    832  e137770b-b0de-4359-9ec7-112b48e40810          Janice Cunningham                  joshuazimmerman@owens.net             Home            But         1              271.69            271.69            Cash    2025-04-16           Ohio            39   Other
    833  078e34b7-c1a7-4e87-9b08-0cb4e7c94737           Cassandra Howard                       jeremy16@edwards.com             Toys          Price         3               33.16             99.48  Mobile Payment    2024-09-23          Texas            46    Male
    834  d53d8227-6c39-46fa-b566-d2cd5bfd8998            Wayne Rodriguez                       bmurillo@hotmail.com           Beauty           Huge         1               73.13             73.13     Credit Card    2024-07-16     California            57  Female
    835  454348b8-f19f-4b0a-87e4-e5d662fd44b7         Benjamin Mcpherson                 jessicabennett@bernard.net             Home         Indeed         5               44.61            223.05  Mobile Payment    2025-01-09   Pennsylvania            31  Female
    836  e0b1cfef-6c70-4f7c-9a09-7b6f921816be                Cindy Smith                      wcallahan@hotmail.com         Clothing           Long         3              303.72            911.16      Debit Card    2024-12-24       New York            66  Female
    837  a6d0444f-68ac-4a8e-913f-522341d17dfd                 Alec Smith                fredericksavannah@yahoo.com      Electronics        However         3              413.29           1239.87          PayPal    2024-09-01     California            26  Female
    838  eea8f86b-8269-4a4e-8c76-c9e91e6d718c              Aaron Sanders                         cshelton@gmail.com         Clothing     Republican         5              331.86           1659.30      Debit Card    2024-05-18       New York            64   Other
    839  78d69575-5b09-4ffa-9e5b-0f5356d7f5e6            Jennifer Walton                      anthonysmith@wood.biz           Sports      Difficult         2              378.71            757.42     Credit Card    2025-04-14       New York            56    Male
    840  9358dd5c-58d0-4649-aa2c-62bc3938c5c0             Zachary Brooks                        ycarrillo@gmail.com           Sports           Push         5               16.45             82.25     Credit Card    2024-06-11           Ohio            63    Male
    841  c55c8ca2-b318-4914-bad5-c4fcf66f383e            Billy Rodriguez                         sandra90@mason.com         Clothing           Must         2              264.49            528.98  Mobile Payment    2024-11-11           Ohio            68  Female
    842  f085f4e0-ad0f-41cb-bbc3-14ddbaadcf11                  Tina Wood                            wvega@yahoo.com           Sports         Modern         2               80.33            160.66     Credit Card    2024-06-02       New York            21   Other
    843  68bfca41-62e6-4618-a75a-fef6713b466c      Mrs. Nancy Jacobs DDS                       heather80@weaver.com             Home            Six         4                8.90             35.60            Cash    2025-01-28       New York            38    Male
    844  acc961fc-b858-4951-98ce-92a9b03d8f26              Ricky Schultz               ojohnson@herman-phillips.net             Toys         Spring         4               62.05            248.20  Mobile Payment    2024-10-20       Illinois            50    Male
    845  8f594c10-71f8-46e1-8611-42d5eaabe44f          Mrs. Hannah Wyatt                    bsmith@hodge-rogers.com         Clothing           Soon         4              260.95           1043.80      Debit Card    2025-01-17          Texas            52   Other
    846  f75bc8d1-00b7-47cf-8b43-e6b0afbfc34a                 Joy Travis                         jmaynard@yahoo.com      Electronics        Pattern         1              216.88            216.88     Credit Card    2025-04-29        Georgia            65   Other
    847  51279764-f612-48e8-8dd4-37c239904c87            Joshua Williams               christopherbarrera@yahoo.com             Toys     Conference         3              119.36            358.08     Credit Card    2024-11-15           Ohio            27   Other
    848  fde286d9-196c-4685-b0cb-af47168773f4                Evelyn Hart               ricardogutierrez@hotmail.com             Home           Trip         5              325.45           1627.25          PayPal    2024-10-11        Georgia            54  Female
    849  290a8369-ae32-4a0a-9603-e1fe0fd10aa7             Stephen Jacobs                        darrell66@gmail.com      Electronics        Against         1               72.70             72.70  Mobile Payment    2024-05-02       New York            32    Male
    850  738f2638-ec52-4365-9205-57ecc69d8fd6                Tina Taylor                   marie80@martin-hurst.net       Automotive          Apply         4               71.45            285.80          PayPal    2024-12-15        Georgia            49   Other
    851  0c023078-2006-4e99-ba92-d3bea273c070                  John Hart                          leroy17@yahoo.com           Sports            Cut         3              206.23            618.69  Mobile Payment    2024-07-06           Ohio            60  Female
    852  e9866131-0451-41b6-a04a-5f83e54e067f             Joshua Roberts                     nicholas49@hotmail.com      Electronics           Goal         1              330.94            330.94  Mobile Payment    2024-07-24        Florida            23  Female
    853  fc571070-42e5-448d-9132-27569554e940                 Tasha King                    davidmartin@simmons.net           Sports        Prepare         4                7.37             29.48          PayPal    2025-02-13       Illinois            25   Other
    854  14bacbeb-0986-4f96-9e99-07aa67b22cb7             Vincent Cooper                         hgarrett@yahoo.com       Automotive           Drug         1              122.04            122.04      Debit Card    2025-03-04        Georgia            68  Female
    855  15921616-c22c-491c-be17-897e09019e2b           Timothy Whitaker                        jessica68@yahoo.com           Beauty          Final         2              197.13            394.26     Credit Card    2025-01-06       New York            53   Other
    856  b7c3516a-0e5c-4906-87f8-55ccd4782b99           Cheryl Hernandez                    morandeanna@hotmail.com      Electronics          Small         2              310.53            621.06  Mobile Payment    2024-07-02       Illinois            31    Male
    857  026d7381-4cb1-463a-a40c-9640f2b8fac4           Charles Stephens              christinesheppard@hotmail.com       Automotive           Mind         4               42.75            171.00     Credit Card    2025-04-03           Ohio            56   Other
    858  71410534-69ee-4b0a-af96-792389bb7640               Barry Carter               nicholas77@johnson-green.com           Sports          Learn         3              377.30           1131.90          PayPal    2025-02-20       Illinois            45  Female
    859  b6fe2b36-9b79-46a3-85b0-2c564e819753               Heather Ford                      christine21@gmail.com         Clothing         People         2              312.30            624.60     Credit Card    2025-03-25        Georgia            20   Other
    860  e8633d2c-20e4-459f-bb33-682bc98d045c              Daniel Parker                         robert76@moore.net        Groceries            Ago         4              344.99           1379.96     Credit Card    2024-12-14        Georgia            27  Female
    861  d0f024df-3f3c-4939-93ae-b4695e3da41f               Anthony Ross                  christopher44@hotmail.com      Electronics         Charge         1              106.28            106.28  Mobile Payment    2024-09-18   Pennsylvania            63   Other
    862  1f62448d-2da2-47cc-98f7-b6fd47577e77               Sharon Clark                         zmejia@hotmail.com         Clothing        Service         5              377.55           1887.75  Mobile Payment    2024-08-06        Georgia            33  Female
    863  3221ec10-7bcb-4361-9526-2cf893c7ca34           Marcus Mason Jr.                         kjohnson@hicks.com      Electronics        Culture         4              351.41           1405.64            Cash    2025-03-03        Georgia            24   Other
    864  6c635e5c-1f19-4a7e-a160-6b8240c17c83               Sarah Brooks                     mccallshelby@gmail.com        Groceries           Feel         3               59.71            179.13            Cash    2024-12-23       New York            26  Female
    865  2f42846c-b8b8-43cd-8af9-4bbce972774e             Madison Barnes                     elliottshane@yahoo.com           Sports           Hope         3              185.04            555.12  Mobile Payment    2024-12-23     California            33  Female
    866  c6f7ee93-059f-4681-a769-3dc285fb942c             Jennifer Bryan                           nscott@gmail.com           Beauty           Case         1              329.80            329.80          PayPal    2024-09-12          Texas            21    Male
    867  cc9f15f5-14f6-40f7-86f7-8c9d4313b1ea                  James Lee                         amybrock@yahoo.com      Electronics         Lawyer         3              474.16           1422.48  Mobile Payment    2024-11-26           Ohio            23   Other
    868  62518b93-8077-4a08-a5d1-fc9f4c87d596             Michael Osborn                         ujones@hotmail.com             Toys       Indicate         5              396.85           1984.25          PayPal    2024-11-23        Georgia            23  Female
    869  4b0692a0-8f7c-4c70-91e5-ca54bd3d736a             Stephanie Long                          lee15@hotmail.com             Toys         Create         1              351.34            351.34      Debit Card    2024-07-08       New York            49   Other
    870  3103f8a8-fefd-48dd-beca-ffb18ead17a4               John Cabrera                        olucero@hotmail.com           Beauty           Race         4              363.64           1454.56          PayPal    2025-04-11        Florida            68    Male
    871  74b96ce1-f34d-42d1-9fcf-9e7920f3e4e0               Amanda Nunez                        umosley@hotmail.com           Beauty          Field         1                7.95              7.95          PayPal    2024-11-02           Ohio            39  Female
    872  83955779-36f2-4d7c-b019-b1741897e3c2            Brittany Turner                      janetzamora@yahoo.com             Home         Within         1              443.84            443.84     Credit Card    2024-10-24          Texas            37    Male
    873  cd31483b-c7be-4e4c-8e2b-537793e24c58  Dr. Stephanie Trevino DVM                     salazardavid@wells.com        Groceries          Early         1              460.52            460.52  Mobile Payment    2025-04-14        Florida            61  Female
    874  eb243602-1905-46dd-b278-196e0256076b               Brian Taylor                   hermanmorgan@vazquez.com        Groceries       Computer         4               31.75            127.00     Credit Card    2024-11-23        Georgia            39   Other
    875  a91d3fa8-1085-4b61-93fe-79a8b6c66b5b                  Sara Chan                     kwatson@gray-ellis.com             Home       Specific         3              168.82            506.46  Mobile Payment    2024-05-23   Pennsylvania            54    Male
    876  16310253-0e55-4f55-8320-f903d693a3cb           Nicholas Jimenez                          april85@ochoa.net           Sports           Best         1              211.66            211.66            Cash    2024-10-10          Texas            38  Female
    877  e7b37bb7-5430-4541-9065-2510ef009bbb                 Lisa Lopez          gregorypark@patterson-johnson.biz      Electronics            Hit         3              211.32            633.96     Credit Card    2024-11-04     California            68  Female
    878  91ff74f3-39ed-4b93-aad4-35185a257428          Mercedes Williams                    elliottamanda@baker.biz         Clothing         Family         1              437.22            437.22  Mobile Payment    2024-05-11           Ohio            68    Male
    879  5569ad28-6ffa-446d-8fc4-540567a4de91              Michael Simon           dianabrown@stevens-gutierrez.org      Electronics      Determine         2              138.31            276.62     Credit Card    2025-04-12        Florida            25  Female
    880  08b92caa-3c1b-4de3-80f2-80aff3040dd2            Stephanie Silva           colemanraymond@roberts-nixon.com           Beauty          Begin         1              440.16            440.16  Mobile Payment    2024-09-07        Georgia            18    Male
    881  af512ae3-0b7e-4f26-8815-817311e64d3c              Natalie Smith                     margaret25@hotmail.com             Home           Area         3              357.90           1073.70  Mobile Payment    2024-05-02       Illinois            32    Male
    882  7fe1a3ca-cb47-408e-ad41-8561427d0aae              Amanda Thomas                     qrodriguez@mahoney.com           Beauty            Man         5              188.14            940.70            Cash    2024-12-27           Ohio            66   Other
    883  0f43de2f-2ca1-4cb4-a230-68b1c26b534c            Laura Velasquez                          nmann@hotmail.com      Electronics           Baby         3              170.76            512.28      Debit Card    2024-10-02       Illinois            61  Female
    884  2d4f4829-e5ef-4108-8b32-2ee006fcd3af               David Sawyer                    meghanstewart@yahoo.com           Sports         Minute         2              487.51            975.02            Cash    2024-10-12     California            58    Male
    885  ecfd2b0c-767c-4f10-8607-6eeb6785f622            Bryan Hernandez         stewartjennifer@flores-flores.info       Automotive          Light         2              307.59            615.18          PayPal    2024-12-14     California            57  Female
    886  cd111eb8-a516-489a-943a-d2c648c22376              Manuel Nelson                     yward@good-aguirre.com           Beauty        Between         2              233.27            466.54  Mobile Payment    2025-04-16           Ohio            40  Female
    887  da9da784-e3c6-4a78-9669-05804c27d09d            Shannon Proctor               shanejohnson@brown-moore.com        Groceries           Same         3               60.71            182.13            Cash    2024-07-30        Georgia            30   Other
    888  09567ad4-c899-4468-b5d0-86c05841d47d                Evan Garcia                michaelsolomon@townsend.com           Beauty              A         5              274.31           1371.55  Mobile Payment    2024-08-27       Illinois            63    Male
    889  babec479-7474-4a13-ba0b-9f90aa9fe737                Kelly James                      lawsoncorey@gmail.com        Groceries           Skin         5               76.62            383.10  Mobile Payment    2024-07-05       Illinois            25   Other
    890  55a7422d-e4a7-4d36-ab62-9b4fe2590971             Michelle Mason                       moorejacob@yahoo.com           Beauty            Bit         5              322.21           1611.05            Cash    2024-05-03           Ohio            57  Female
    891  635a73e8-0839-4f7d-af65-eced565ae093            Kristina Bolton                          susan22@gmail.com           Sports            Too         4              230.12            920.48      Debit Card    2024-10-16          Texas            36    Male
    892  b7c9f625-cfaa-4501-9ffb-509f3d36d163               Lisa Lindsey                             troy04@kim.com      Electronics           Site         2              393.14            786.28     Credit Card    2024-10-18   Pennsylvania            28    Male
    893  15eef487-2dbf-4035-b512-d3e3b20e5ec0              Edward Harris                   jdixon@holden-morgan.org           Beauty         Almost         2               25.52             51.04          PayPal    2024-12-30        Florida            69   Other
    894  9c215a4a-ac22-4ebd-a0b2-69ef20d03f24            Brooke Thompson                  steven75@hardy-flores.com           Sports        Billion         2               66.98            133.96     Credit Card    2024-06-27       Illinois            28   Other
    895  fcba9cd1-eaf5-4ae0-abe7-f1673b2a61a1             Julie Schwartz                     smallkayla@hotmail.com        Groceries          Agree         5              455.24           2276.20      Debit Card    2024-06-26       New York            65   Other
    896  0033503f-5e10-4ea0-9514-654ffb7f2383                 Emma Jones                        millsadam@bowen.com           Sports    Traditional         1              309.85            309.85          PayPal    2024-08-03     California            27   Other
    897  6231e5e6-48dc-4f93-8201-8def0bfc40ea              James Allison                 garciajacqueline@yahoo.com             Toys           Test         2              322.66            645.32          PayPal    2025-01-28        Florida            34    Male
    898  5a93e1c4-63c1-4d0a-87bc-241c9eb56b2e             Anthony Lester                       robbinsamy@yahoo.com             Toys       Together         5               75.22            376.10      Debit Card    2024-07-31          Texas            33   Other
    899  b3c9aa4a-8d6f-417d-842d-5303bbfd37c7         Roberta Richardson                        ralph16@hotmail.com           Beauty             Up         1               63.30             63.30            Cash    2025-02-09       Illinois            45    Male
    900  f697dc86-b918-4286-a2ff-33af43659f06              Robert Howard                mcknightbarbara@hotmail.com       Automotive          Model         3              439.04           1317.12     Credit Card    2024-11-26           Ohio            70   Other
    901  87ae78dc-eb96-4452-82bf-5b9052b8270a              Tamara Morgan                     rebeccadavis@gmail.com             Toys          Field         3               10.31             30.93            Cash    2024-10-27   Pennsylvania            19   Other
    902  001ccead-0995-47e8-875f-b2035742e04e              Susan Solomon                        moodyanita@wolf.biz           Beauty         Recent         3              173.52            520.56            Cash    2025-04-19          Texas            31   Other
    903  5fbf3537-fc75-43b8-9c66-97ef6b8e69bb              Lori Martinez                           dmills@gmail.com             Toys          Watch         2               56.92            113.84     Credit Card    2025-02-18       Illinois            23   Other
    904  365dd8cd-c7a0-4f63-8564-523a94b3bf6a              Timothy Perry                   qhines@ryan-delacruz.net      Electronics          Issue         5               90.31            451.55  Mobile Payment    2025-04-06        Florida            56    Male
    905  e910f946-d3de-4fde-ab62-f316d7d29fc8           Frank Rodgers II                 brenda86@james-salazar.org           Sports           Face         1               55.38             55.38  Mobile Payment    2024-07-31        Florida            67  Female
    906  79655d07-225d-43ee-9bf1-ce3636b47ac2               Kelly Taylor                       cynthia00@juarez.com        Groceries           Wish         3              229.50            688.50  Mobile Payment    2025-04-30       New York            34   Other
    907  b6fa501b-74e2-4419-a4cc-63b5dd769eeb             David Ferguson                         hperez@hotmail.com      Electronics           Food         1               47.19             47.19      Debit Card    2025-03-07           Ohio            70    Male
    908  ded10ecb-30e9-4f0a-a6b4-8947fdea6307             Steven Andrews                         jake69@hotmail.com        Groceries      Treatment         2               51.64            103.28     Credit Card    2024-06-13     California            49    Male
    909  3ca0ea9c-b552-4e2e-87b9-d2a29655863a                 Stacey Fox                     daviskristin@yahoo.com      Electronics          Avoid         2              365.65            731.30          PayPal    2024-06-01        Florida            60    Male
    910  a0f7dde4-91b8-40bc-90c6-de6942269ba2            Erica Wilkinson           christiancarter@rich-wilson.info        Groceries       Anything         4              246.88            987.52     Credit Card    2025-04-22       New York            45   Other
    911  dabc29e6-14f7-447e-975b-dbf16e02cb15            Stephanie Jones                        smitchell@gmail.com         Clothing          Exist         3              184.34            553.02      Debit Card    2024-06-11       New York            46   Other
    912  9c2be42f-a2df-413d-8b89-3c4e6f5dce30             Hunter Acevedo                   garciakimberly@yahoo.com         Clothing            Put         2               16.86             33.72      Debit Card    2024-07-07       Illinois            45    Male
    913  7f1fe0e0-ce14-4ace-a2f5-6451d8afa83f               Janet Turner                         ricky13@garcia.com           Beauty          Break         1              174.00            174.00          PayPal    2024-07-15   Pennsylvania            57    Male
    914  916f1cf0-cf19-4cb0-8486-e5f6146c52bc               Terry Parker                  richardbradford@yahoo.com         Clothing          Board         5              433.53           2167.65            Cash    2024-09-02   Pennsylvania            56  Female
    915  89df1d31-1c74-4c71-a8f4-b7d9fa18c920            Michelle Torres                         xgarcia@castro.com       Automotive      According         2              207.98            415.96  Mobile Payment    2024-10-19   Pennsylvania            40  Female
    916  3d3662cc-1374-4672-8acc-2d90da29e24d          Kathryn Contreras          lindabecker@mcbride-carpenter.biz           Sports         Behind         3              113.59            340.77  Mobile Payment    2024-05-06        Florida            21  Female
    917  a989c93e-cb78-4a3b-95af-af76b74100cd               Denise Moore                          alan15@turner.net        Groceries           Whom         5               74.21            371.05            Cash    2024-06-27       New York            47   Other
    918  5599a632-21d1-4526-9444-9233c82a0999               Ryan Johnson               belinda93@robertson-king.com             Toys         Parent         1              394.45            394.45      Debit Card    2024-05-16     California            51   Other
    919  ed8dedb9-261e-453d-b24a-f5c450c34f7d            Yolanda Bonilla                            mross@gmail.com             Toys          Adult         3              424.26           1272.78  Mobile Payment    2024-08-12        Georgia            33   Other
    920  f624868f-c732-4219-867a-4dc830a7b65a               Samuel Heath                         robert61@yahoo.com       Automotive           Risk         1              430.14            430.14          PayPal    2024-05-28     California            67  Female
    921  0ab9c996-c93c-48d9-8a72-c1609efeb21e               Melissa Boyd                          randy22@gmail.com       Automotive          Among         3              257.09            771.27  Mobile Payment    2025-02-09        Florida            33  Female
    922  8323aa20-4d99-4076-ab24-8c39cb3c6ee8                 Adam Lucas                        rwilliams@gmail.com         Clothing        Without         4              240.49            961.96  Mobile Payment    2025-02-25        Georgia            57  Female
    923  ef3bd850-f72c-4672-b5fb-124fcceb28a7                John Willis                       grahamjake@yahoo.com             Home          Voice         4              322.68           1290.72  Mobile Payment    2024-07-17   Pennsylvania            57    Male
    924  6765f0fc-15ba-45d2-98d9-326fbe5833e6               Miguel Smith             taylorrobert@henry-edwards.com             Home            Old         4              350.85           1403.40     Credit Card    2024-10-26        Georgia            61    Male
    925  cf5d5422-7cbe-4d01-8349-3e8f58d25753             Robert Ramirez                  stephensloretta@gmail.com         Clothing          Small         3              178.68            536.04            Cash    2025-03-04          Texas            66  Female
    926  a5a7a408-7683-4600-a718-1287bbb03e4a             Maureen Cherry               meganwallace@jones-ramos.com      Electronics            Run         5               13.06             65.30     Credit Card    2024-07-10       New York            19    Male
    927  b98ac610-97d1-4ad6-88de-7b1ef946619c                 Barry King                     jking@reese-green.info         Clothing           Well         1              278.28            278.28      Debit Card    2025-04-09       New York            20   Other
    928  fe97e28c-b614-40bd-a75d-2d303e781b03            Patricia Thomas                     justinpayne@pierce.com             Toys         Affect         1               16.58             16.58     Credit Card    2024-09-10        Georgia            60  Female
    929  040ccf30-0bcb-40a9-ab27-cae3f92a6e4d                Duane Smith                 loweryfrederick@rivera.net             Toys             Or         3              377.90           1133.70      Debit Card    2024-07-02       New York            19    Male
    930  7f7b7683-0448-41b0-8c75-2d60a683e9d8                Dakota Lang                      caitlin82@hotmail.com             Toys            Day         2              193.28            386.56     Credit Card    2024-11-20           Ohio            51  Female
    931  fa79f3fc-dccf-4ae5-a042-218229f56d1f             Matthew Spence                   christinebrown@white.com           Sports        Country         4              241.87            967.48          PayPal    2024-10-06        Georgia            25  Female
    932  ad776487-d071-4e66-a5c5-2567391a9321          Mr. Stephen Ortiz                      nanderson@hotmail.com           Sports          Eight         5              230.19           1150.95     Credit Card    2025-01-24        Florida            57  Female
    933  975ec708-16b5-42ab-97d7-f81d98a1e292           Elizabeth Finley                         tclark@warren.info         Clothing          Range         2              337.64            675.28  Mobile Payment    2024-10-24   Pennsylvania            21  Female
    934  bb51bcb1-d23b-4cb1-9c69-18691a351fd8          Christopher Wyatt                         hbryan@hotmail.com             Home     Management         2               68.05            136.10            Cash    2024-09-29       Illinois            19   Other
    935  2d3e5974-499a-4c1b-b1b4-5606228b21f0               Lauren Wiley                         james52@brown.info             Toys           Task         1               56.40             56.40     Credit Card    2024-06-17        Florida            42   Other
    936  5f6e4f3e-d6c2-4f64-9a12-f1b7b8984fb8                 Tami Baker                   toddmitchell@hotmail.com           Sports         Senior         5              459.15           2295.75  Mobile Payment    2024-08-27           Ohio            30    Male
    937  e040a898-ba37-438c-a240-ef532c66a67b            Michael Wallace                         nwallace@yahoo.com      Electronics        Discuss         1              287.68            287.68      Debit Card    2025-01-28           Ohio            51    Male
    938  138adef8-a64f-4dcf-bb30-10f87fb37534                Alex Lawson                        jessica57@yahoo.com             Home         Parent         4              115.45            461.80  Mobile Payment    2024-12-31           Ohio            33   Other
    939  34d84137-21db-4c06-ba21-6e71e6142460             Joseph Mahoney                        xnorton@salazar.com        Groceries          Thing         1              147.25            147.25          PayPal    2024-05-17           Ohio            50  Female
    940  46546525-5497-489b-b46f-f693938e01a8               Blake Taylor                      ruizscott@hotmail.com         Clothing          House         4              425.67           1702.68          PayPal    2024-10-21   Pennsylvania            34  Female
    941  7a9775f4-5ca9-4d85-85c9-da2ccc20c12a               Travis Garza          johnstoncrystal@gates-collins.com             Toys     Difference         5               48.15            240.75  Mobile Payment    2024-05-11           Ohio            48   Other
    942  4f69c091-55b5-482c-9029-717b8c87dc4f                 Dawn Chase                  sweeneydeanna@hotmail.com           Sports      Community         4               86.06            344.24            Cash    2025-04-30        Georgia            53    Male
    943  3af9d558-0d19-4e22-a9b7-08ce686c3843                Daniel Cole                     moranmelanie@yahoo.com      Electronics           Mean         1               75.37             75.37          PayPal    2025-03-14     California            48  Female
    944  9e689033-a934-4bb4-9dd6-d2b98593c42f               Rachel Smith                 harryferguson@mitchell.org       Automotive         Second         5              475.78           2378.90          PayPal    2025-02-24       New York            46   Other
    945  d487388a-1069-41c5-9e31-557866a9985e               Andrew Nunez                      danastevens@white.com      Electronics            Nor         3               65.52            196.56          PayPal    2025-01-27       Illinois            50    Male
    946  5009429a-2f8e-44bb-b235-9ec31b7dfaf4             Angela Stewart                     rickygordon@rivers.com           Sports           Hold         5              157.89            789.45     Credit Card    2024-08-01        Florida            45    Male
    947  0b574f9a-4ebd-4257-aa39-590d44a4c41e              Beverly Perez                       joannhall@morgan.biz       Automotive          Apply         4              218.82            875.28     Credit Card    2024-05-13          Texas            28    Male
    948  49f49e44-91b4-40fd-8f74-26272d0f04d3                Keith Smith                    berrykathryn@levine.com             Home          Think         3               88.93            266.79            Cash    2024-10-19       Illinois            53  Female
    949  bf30349d-75b2-4202-b9b0-ad44642b6518             Jillian Knight                           qford@larson.com           Sports           Open         3               56.00            168.00     Credit Card    2024-07-15   Pennsylvania            48  Female
    950  d94415fe-b19b-43a2-90b0-6b6573a812e2             Michael Moreno                         andrew91@munoz.com       Automotive        Quickly         3              240.59            721.77          PayPal    2024-10-31       Illinois            37   Other
    951  0eb8a07c-e0e4-42c4-a4ca-415c7a12ff32               Jackie Reese            montgomerymichael@middleton.com         Clothing           Stay         1              394.51            394.51            Cash    2024-11-19     California            70    Male
    952  7a52fdbe-dda7-401e-959b-7b5022757e00               Samuel Ellis                      jcampbell@simmons.com           Beauty         Reason         2              482.64            965.28      Debit Card    2024-12-31        Florida            56  Female
    953  16befc0e-7573-4ca2-bc1f-9967b3204509                Ian Salinas                       deanna27@hotmail.com             Home          Court         3              277.37            832.11          PayPal    2024-06-08     California            63   Other
    954  d5096d07-34dd-40a1-a7ec-2fe2ee8b0e5c          Courtney Reese MD                         lucas97@morton.biz       Automotive          Leave         2               99.06            198.12  Mobile Payment    2024-08-01        Georgia            19   Other
    955  3df8abb1-926b-4a2e-9741-5e20f055f118               Lauren Kline                   kathy94@stark-moyer.info           Sports           Make         5              318.92           1594.60     Credit Card    2024-09-22          Texas            43    Male
    956  72dbdbef-b31c-4d80-91b8-485956f9cdd3             Caitlin Carter                        chamilton@yahoo.com       Automotive          Front         2              240.44            480.88     Credit Card    2024-05-21       Illinois            37    Male
    957  442e9312-17b2-4515-8afd-93902405b218              Daniel Porter                     njohnson@henderson.com           Beauty            Two         5               36.72            183.60  Mobile Payment    2024-05-12        Georgia            67  Female
    958  b5112130-91a2-460d-ab7c-209b34b8b346               David Patton               samantha18@jones-morales.com         Clothing          Their         3               73.32            219.96      Debit Card    2024-08-24   Pennsylvania            43   Other
    959  b5f2af01-5437-4106-ad69-a0ac935dcc14              Debra Hoffman                    georgediaz@espinoza.com        Groceries         Pretty         5              389.33           1946.65     Credit Card    2024-07-04     California            64    Male
    960  fea3360f-96f3-44ef-b05e-51ce6a04d41b               Colleen Hood                       rcoleman@hotmail.com       Automotive         Spring         3              326.12            978.36          PayPal    2024-09-13           Ohio            28   Other
    961  1cd3d3d9-07e5-4ee9-b9d2-3456de2e13a7           Cassandra Barker                           triley@yahoo.com       Automotive          Color         3              373.54           1120.62  Mobile Payment    2024-12-28     California            44  Female
    962  5a1f2bc2-382b-43dc-8d31-f5a6376d6d02            Gregory Johnson              dthompson@schmidt-nelson.info         Clothing            Law         3               22.80             68.40          PayPal    2025-01-09       New York            61   Other
    963  460d8bbd-16b2-4238-858e-f10c12e5527a            Amanda Mitchell                         ronald68@gmail.com        Groceries         Senior         1              300.62            300.62            Cash    2024-08-23       New York            51    Male
    964  16d5b465-23f2-407e-8e75-ebd15debafea        Mackenzie Dominguez                 ostephens@mcneil-baker.com       Automotive          Style         5              262.16           1310.80  Mobile Payment    2024-05-30   Pennsylvania            48   Other
    965  2470c3f3-620b-4634-b3de-d6a3e4a1f988           Michael Campbell                     youngerica@hotmail.com      Electronics           Cost         2              485.41            970.82            Cash    2025-04-04        Georgia            49    Male
    966  313fa5a5-60b7-41b0-b2d5-af8318a92253           Kristine Johnson                  andreaoconnor@fischer.com       Automotive       Democrat         2              182.50            365.00      Debit Card    2024-12-15           Ohio            46  Female
    967  1c8c33b5-c7c9-484f-9456-066e1979f305              Juan Arellano                      phelpsrobin@yahoo.com       Automotive          Study         3               89.81            269.43          PayPal    2024-12-05          Texas            51   Other
    968  9b9dfed9-e5a8-4591-b3f5-5b4a36b2a962              Alyssa Harris                     williamskyle@yahoo.com             Home      Community         5               94.42            472.10            Cash    2024-09-23     California            38    Male
    969  877592f8-7de1-4901-af84-1560b77879e2                Heidi Mccoy                       cheryl04@hotmail.com        Groceries             My         2              106.15            212.30  Mobile Payment    2024-07-25       New York            45    Male
    970  219658e5-41dc-4391-b348-f25000aa886d             Travis Gilbert         josephwilliams@figueroa-miller.com           Beauty     Democratic         3              484.82           1454.46      Debit Card    2024-10-01   Pennsylvania            21    Male
    971  913f4b50-625d-4fd7-9a56-90fca763bb85               Nichole Ward           taylorjohnson@hansen-swanson.com             Toys            Cut         3              269.73            809.19            Cash    2024-11-27       Illinois            19  Female
    972  c1759c9d-1d86-4a25-bb80-286128097136              Chris Jenkins                          aweaver@gmail.com      Electronics      Candidate         2              333.45            666.90          PayPal    2025-04-18        Florida            42  Female
    973  d6486d72-2692-4859-9d57-481537cf6919              Connor Rivera                          operez@guzman.biz           Beauty          Three         3              291.27            873.81      Debit Card    2025-03-20        Georgia            64    Male
    974  63519817-15d0-414b-84da-7463de494de5               Alexander Ho                 pamela86@kelly-barnett.org           Beauty          Along         3              269.81            809.43          PayPal    2025-03-29           Ohio            38    Male
    975  65ed91ed-fc16-4674-9985-ff71d30cb89a              Jason Sherman                       littlejohn@gmail.com             Toys         Letter         5               33.68            168.40          PayPal    2024-07-18          Texas            22    Male
    976  f8b5da69-c748-45f7-9cf0-6416090a6d9b            Jeffrey Andrews                          renee76@gmail.com           Beauty         Debate         3              354.00           1062.00  Mobile Payment    2024-06-18          Texas            32  Female
    977  7428b3a0-e558-4306-86ed-f92691e9ba43              Steven Rivera                           sara62@gmail.com         Clothing        Quality         2              373.36            746.72      Debit Card    2025-03-18       New York            28   Other
    978  6ee84a1d-768b-49dd-b652-b029bc2d193a           Jennifer Simpson                        kingtodd@miller.com           Beauty          Range         3              393.75           1181.25            Cash    2024-12-04          Texas            37  Female
    979  38c00855-b995-4698-afa8-4d95ea162b6a            Reginald Carter                   strongmarcus@hotmail.com           Sports           Pull         4              237.97            951.88  Mobile Payment    2025-01-10        Georgia            20  Female
    980  973be64f-816b-404d-acba-0594ee0a7016               Patrick Diaz              kristenbowen@brown-parker.com       Automotive            End         4              128.34            513.36  Mobile Payment    2024-08-30       Illinois            45    Male
    981  38280998-a552-474a-9a54-8bcd915ea946             Tiffany Flores                            vwood@gmail.com             Toys           Your         3              167.10            501.30     Credit Card    2024-07-23     California            54   Other
    982  97412311-a086-4629-9e1c-e7e13f267d0e            Russell Griffin                     moorebrittney@wise.net             Home     Generation         5              392.02           1960.10  Mobile Payment    2024-06-13          Texas            70  Female
    983  f360cdab-ae7f-4849-b076-ce6b147f9780                John Travis                    davidorozco@hotmail.com             Home         Within         4              291.97           1167.88      Debit Card    2025-05-01       Illinois            21   Other
    984  9b8f0a10-53f2-496b-8afe-60be82754ad5               Raymond Ward                 micheleconley@villegas.com      Electronics           Must         5               79.88            399.40      Debit Card    2024-07-18        Georgia            19    Male
    985  614ed21e-9916-4ba4-acd7-28d545f53edc              Monique Burns                   wilkinscindy@hotmail.com             Toys         Likely         2              195.06            390.12          PayPal    2025-03-30       Illinois            53    Male
    986  b0dd7383-6d64-4675-b3f7-d47e7aff7b17              Nicholas Webb                    jamesorozco@hotmail.com           Sports       Anything         2              198.42            396.84          PayPal    2024-06-15       Illinois            27    Male
    987  e20aaffd-6d58-4fb0-b56a-a4aa748e38c5              Lisa Schaefer                  nicholasevans@hotmail.com             Toys         Senior         3              225.13            675.39            Cash    2024-09-11     California            31    Male
    988  dfcd04b6-cca6-4d21-a37b-a33f63d5beaa            Michele Jackson                          kevin92@yahoo.com       Automotive            Per         3              488.13           1464.39  Mobile Payment    2024-07-12       Illinois            25   Other
    989  f1b39bec-8935-423d-af71-af51f791d400          Ashley Jenkins MD                      wendyreed@hotmail.com           Beauty        Society         2              181.41            362.82      Debit Card    2024-12-11           Ohio            39   Other
    990  6e51acc5-5be8-4791-99b6-b2918f7421b6                  Ryan Wood                      juliataylor@gmail.com        Groceries        Medical         1              111.12            111.12          PayPal    2025-01-20        Florida            24    Male
    991  e28304ee-9fcd-442b-b6f2-123cfbfa625a                Lisa Murphy                        moodyerin@gmail.com       Automotive        Country         3               40.76            122.28     Credit Card    2024-12-18           Ohio            26    Male
    992  24429e0a-fb36-47d7-9335-25c9681c7293              Jacob Collins                     sallybarker@harris.org      Electronics         Should         1              198.41            198.41          PayPal    2025-02-05        Georgia            24  Female
    993  a81d19ae-3878-4cc6-bd9d-74a1aa147780               Katie Taylor                         sarah74@rogers.com             Toys         Growth         2              428.51            857.02            Cash    2024-10-05          Texas            62    Male
    994  1734abfc-7d04-4e69-848b-c9004a6b586a             John Hernandez                 martinezjennifer@dixon.com           Beauty           Face         2              440.00            880.00  Mobile Payment    2025-02-10   Pennsylvania            62    Male
    995  5cc30e92-9743-4a6a-8542-b0d97bb6b5fb                James Marsh                 deborahbuchanan@morris.com             Toys          Phone         5              377.15           1885.75            Cash    2024-09-09   Pennsylvania            34   Other
    996  338f3773-3fa1-4ae5-96ae-f4a51f7876fc            Johnathan Brown                           mary67@gmail.com             Home         Choice         1               93.86             93.86          PayPal    2024-07-03           Ohio            35    Male
    997  85a59a5f-44fd-4635-97e8-cb64f0b0ef89           Jason Powell PhD                           paul88@yahoo.com        Groceries          Avoid         1               55.81             55.81      Debit Card    2025-01-31   Pennsylvania            54   Other
    998  9d5fa8e1-b058-462e-9d94-788e9824b448              Emily Salazar                         vbrady@hotmail.com      Electronics        Partner         5              218.61           1093.05      Debit Card    2024-09-17       Illinois            43   Other
    999  a2dd6672-21cf-4a8f-b45c-0746d7a38640         Stephanie Santiago                           vyoung@smith.com           Sports       National         4              181.38            725.52      Debit Card    2025-01-20        Florida            26    Male
    


```python
# Explore and Analyze the Data
df['Transaction ID'].value_counts()
```




    1e7985ef-741e-4437-a81d-bf7e7311e863    1
    9dba4eae-a566-4d45-a01a-81e56a81584a    1
    cd94ffb5-cdda-4126-a89b-562e55bc0f16    1
    6d25fe49-c955-4639-a3a7-0397f3f82c61    1
    67939266-41d5-4d65-8710-29fa6b14e139    1
                                           ..
    eada0014-3888-43c9-bef9-141f444c3f1a    1
    01e2a742-3379-4b07-bc50-75a936e1e4b2    1
    547356ea-6e7d-47b4-b864-d2e5254b05ad    1
    7fe1a3ca-cb47-408e-ad41-8561427d0aae    1
    d2331a8b-2ebe-4a44-8222-a23edb0f7884    1
    Name: Transaction ID, Length: 1000, dtype: int64




```python
print(df.duplicated()) #check for duplicated rows
```

    0      False
    1      False
    2      False
    3      False
    4      False
           ...  
    995    False
    996    False
    997    False
    998    False
    999    False
    Length: 1000, dtype: bool
    


```python
# Finding Relationships correlation 
correlation = df.corr()
sns.heatmap(correlation, annot=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1671aaea4c0>




![png](output_7_1.png)



```python
Total_global = df['Total Amount ($)'].sum()
print("le chiffre d'affaire globale des transactions égale à",CA_global,'$')
```

    le chiffre d'affaire globale des transactions égale à 711810.4 $
    


```python
# Calcul du chiffre d'affaires par genre
ca_par_genre = df.groupby('Gender')['Total Amount ($)'].sum()
print(ca_par_genre)
```

    Gender
    Female    238194.18
    Male      243508.78
    Other     230107.44
    Name: Total Amount ($), dtype: float64
    


```python
# Histogramme
ca_par_genre.plot(kind='bar', color=['skyblue', 'lightcoral'])
plt.title("Chiffre d'affaires par genre")
plt.ylabel("Total Amount ($)")
plt.xlabel("Genre")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()
```


![png](output_10_0.png)



```python
# Somme de la colonne 'Total Amount ($)' pour les clients âgés de 18 à 30 ans
total_18_30 = df.loc[(df['Customer Age'] >= 18) & (df['Customer Age'] <= 30), 'Total Amount ($)'].sum()
print("Le chiffre d'affaires généré par les clients entre 18 et 30 ans est de", total_18_30, "$")
```

    Le chiffre d'affaires généré par les clients entre 18 et 30 ans est de 178240.85 $
    


```python
# Somme de la colonne 'Total Amount ($)' pour les clients âgés de 30 à 60 ans
total_30_60 = df.loc[(df['Customer Age'] > 30) & (df['Customer Age'] <= 60), 'Total Amount ($)'].sum()
print("Le chiffre d'affaires généré par les clients entre 30 et 60 ans est de", total_30_60, "$")
```

    Le chiffre d'affaires généré par les clients entre 30 et 60 ans est de 402321.52 $
    


```python
# Somme de la colonne 'Total Amount ($)' pour les clients âgés de plus de 60 ans 
total_60 = df.loc[(df['Customer Age'] > 60), 'Total Amount ($)'].sum()
print("Le chiffre d'affaires généré par les clients agés plus de 60 ans est de", total_60, "$")
```

    Le chiffre d'affaires généré par les clients agés plus de 60 ans est de 131248.03 $
    


```python
chiffre_affaire_age = {
    '18-30': 178240.85,
    '30-60': 402321.52,
    '60+': 131248.03 
}

# Convertir en deux listes
tranches = list(chiffre_affaire_age.keys())
montants = list(chiffre_affaire_age.values())

# Tracer l'histogramme
plt.figure(figsize=(10,6))
plt.bar(tranches, montants, color='skyblue')
plt.title("Chiffre d'affaires par tranche d'âge")
plt.xlabel("Tranche d'âge")
plt.ylabel("Chiffre d'affaires ($)")
plt.tight_layout()
plt.show()
```


![png](output_14_0.png)



```python
print(df['Customer State'].unique())   #Afficher les states uniques
```

    ['Illinois' 'Pennsylvania' 'Florida' 'Georgia' 'Texas' 'Ohio' 'California'
     'New York']
    


```python
# Grouper par état et sommer la colonne 'Total Amount ($)'
chiffre_affaire_par_state = df.groupby('Customer State')['Total Amount ($)'].sum().sort_values(ascending=False)

# Affichage
print(chiffre_affaire_par_state)
```

    Customer State
    Texas           109841.31
    Ohio             98893.71
    California       95673.81
    Georgia          87980.99
    Illinois         84710.84
    New York         80221.94
    Florida          77459.80
    Pennsylvania     77028.00
    Name: Total Amount ($), dtype: float64
    


```python
data = {
  "Customer_state": ['Texas','Ohio','California','Georgia','Illinois','New York','Florida','Pennsylvania'],
  "chiffre_affaire_par_state($),": [109841.31, 98893.71, 95673.81, 87980.99, 84710.84, 80221.94, 77459.80, 77028.00 ]
}

#load data into a DataFrame object:
df1 = pd.DataFrame(data)

print(df1) 
```

      Customer_state  chiffre_affaire_par_state($)
    0          Texas                     109841.31
    1           Ohio                      98893.71
    2     California                      95673.81
    3        Georgia                      87980.99
    4       Illinois                      84710.84
    5       New York                      80221.94
    6        Florida                      77459.80
    7   Pennsylvania                      77028.00
    


```python

# Histogramme (barres verticales)
chiffre_affaire_par_state.plot(kind='bar', figsize=(12,6), color='skyblue')

plt.title("Chiffre d'affaires par État")
plt.xlabel("Customer State")
plt.ylabel("Total Amount ($)")
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)

plt.tight_layout()
plt.show()
```


![png](output_18_0.png)



```python
# 1. S'assurer que la colonne de date est au bon format
df['Purchase Date'] = pd.to_datetime(df['Purchase Date'])

# 2. Grouper par date (ou par mois/année si tu préfères) et sommer le chiffre d'affaires
chiffre_affaire_temps = df.groupby('Purchase Date')['Total Amount ($)'].sum()

# 3. Tracer le diagramme en courbes
plt.figure(figsize=(12,6))
plt.plot(chiffre_affaire_temps.index, chiffre_affaire_temps.values, marker='o', linestyle='-')
plt.title("Évolution du chiffre d'affaires dans le temps")
plt.xlabel("Date de transaction")
plt.ylabel("Chiffre d'affaires ($)")
plt.grid(True)
plt.tight_layout()
plt.show()
```


![png](output_19_0.png)



```python
# 1. Conversion de la date si ce n'est pas encore fait
df['Purchase Date'] = pd.to_datetime(df['Purchase Date'])

# 2. Extraire l'année dans une nouvelle colonne (optionnel mais utile)
df['Year'] = df['Purchase Date'].dt.year

# 3. Filtrer et sommer pour 2024
total_2024 = df.loc[df['Year'] == 2024, 'Total Amount ($)'].sum()

# 4. Filtrer et sommer pour 2025
total_2025 = df.loc[df['Year'] == 2025, 'Total Amount ($)'].sum()

# 5. Affichage
print("Chiffre d'affaires en 2024 :", total_2024, "$")
print("Chiffre d'affaires en 2025 :", total_2025, "$")

```

    Chiffre d'affaires en 2024 : 468953.12 $
    Chiffre d'affaires en 2025 : 242857.28 $
    


```python

```
