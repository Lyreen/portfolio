Data was sourced from Kaggle and was pre-cleaned. After duplicating the original file, on the working sheet, income bracket (with USD currency, under $20k is poverty, under $60k is average, $100k is high, and above $150k is very high) and age bracket (16+, 23+, 30+, 45+) were created. Brackets are created to reflect closest life changing events, such as 23+ is typical fresh grad age, $100k is a six-figure, typically comfortable income bracket, 30+ is when new families are established, etc.

Income bracket: =IFS(D2>149000, "Very High", D2>99000, "High", D2>59999, "Average", D2>19999, "Low", D2>0, "Poverty") <br>
Age bracket: =IFS(M2>59, "Pension Age", M2>44, "Elderly (45+)", M2>29, "Middle Age (30+)", M2>22, "Adult (23+)", M2>15, "Teen/Young Adult (16+)")


<img width="1871" height="806" alt="image" src="https://github.com/user-attachments/assets/fb5bd9ff-dc2f-414a-ac4a-9d77ed932bde" />

A dashboard of Bike Sales in Europe, North America, and Pacific with a simple dashboard that spotlights on the largest target market. <br>
The findings revealed that while families and individuals of low and average income make up the biggest sales number, **low-income families** specifically in the North American region are **highly unlikely to purchase the product** compared vs. those of high-income, a unique behavior not seen in other regions such as the Pacific and Europe. The latter in fact shows very similar buying percentage in both average and high-income brackets. <br>
In the Pacific region where the minimum wage is lower, the market sees higher buying percentage within low and poverty-level income bracket. <br>

This prompts several possibilities and deeper explorations for the potentials of expanding market into certain regions or solving the conundrum of low sales, yet high bike ownerships:
- The possible existence of **long-standing competitors** that has solidified their positions as trusted retailers in North America.
- **Adults under 30** are less likely to get a bike. Analyze this behavior, as new emerging adults and mostly job-seeking fresh grads, a bike should be a favored, cheaper means of transportation.
- Average income bracket in the Pacific region needs to be further explored.
- In-depth analysis as to **why lower-income bracket in the North American region do not own a bike** may provide the solution to turn it into a profitable market, a head start in mining the new, ignored vein.
- **Men are more likely to buy bikes**, especially men who are over 45+ and married, ads targeting this bracket should be increased.
