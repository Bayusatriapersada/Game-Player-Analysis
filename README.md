# Game-Player-Analysis
A repo for Probability and stochastic processing, and Data Analysis for game players and its data story
by
* Bayu Satria Persada              (1706985924)

OVERVIEW
* [Description](#Description)
* [Predicting](#Predicting)
* [Notebook](https://github.com/Bayusatriapersada/Game-Player-Analysis/blob/master/Game_Player_analysis.ipynb)
* [Presentation]()


## Description
### CS:GO
CSGO merupakan game FPS (First Person Shooter) yang dibuat oleh Valve dan Hidden path Entertainment, CS:GO merupakan seri ke empat dari Counter Strike , dan baru di release pada tahun 2014. Semenjak game ini dilaunch di Steam , CS:GO terus mengundah banyak player baru  yang setiap bulannya lebih dari ratusan ribu pemain, Bisa di katakan bahwa CS:GO merupakan game terbesar di bidang FPS yang terdapat di Steam market.

### Rainbow Six Siege
Rainbow Six siege (R6) merupakan salah satu seri dari Tom Clancy’s Rainbow six series, yang merupakan Online Tactical Shooter dan bisa disebut juga First Person Shooter yang di kembangkan oleh Ubisoft dan di release pada tahun 2015, tepatnya pada 1 Desember 2015.
Rainbow Six Siege setelah launchnya diberikan title oleh kritikus game tertentu sebagai salah satu game multiplayer terbaik di pasar modern karena update updatenya setelah di launch
dari kedua dasar game tersebut saya ingin menemukan titik korelasi antara kedua game ini, karena saya memiliki hipotesa bahwa game memiliki karakteristik yang sama halnya seperti sebuah musik, ketika seseorang bosan dengan musik dengan genre tertentu maka orang itu akan mencari musik baru dengan genre yang sama, dan kemungkinannya lebih besar, begitu juga dengan Game.

Maka akan dilakukan prediksi dengan menggunakan Facebook Prophet

## Predicting
Prediksi dilakukan dengan hal yang mudah yaitu pertama memasukan data dan lalu di olah sehingga menjadi data yang berisikan tanggal dan jumlah ataupun nilai lainnya

kemudian masukan hari libur dan event secara manual dan juga secara automatis dari prophet itu sendiri
```
summer = pd.DataFrame({
        'holiday': '2 window',
        'ds' :pd.to_datetime(
            ['2017-09-22','2018-09-23','2019-09-22']),
        'lower_window' : -92,
        'upper_window' : 0,       
    })
summersale = pd.DataFrame({
        'holiday': '2 window',
        'ds' :pd.to_datetime(
            ['2017-06-22','2018-06-22','2019-06-22']),
        'lower_window' : 0,
        'upper_window' : 14,       
    })
wintersale = pd.DataFrame({
        'holiday': '2 window',
        'ds' :pd.to_datetime(
            ['2017-12-21','2018-12-21','2019-12-21']),
        'lower_window' : 0,
        'upper_window' : 13,       
    })
holidays = pd.concat((summer, summersale,wintersale))
m = Prophet(holidays=holidays,holidays_prior_scale=20)
p = Prophet(holidays=holidays,holidays_prior_scale=20)
p.add_country_holidays(country_name='US')
m.add_country_holidays(country_name='US')
p = p.fit(df2)
m = m.fit(df)
```
lalu tinggal prediksi sesuai kemauan , contoh hanya dilakukan untuk 1 tahun kedepan
```
R6futureplayer = m.make_future_dataframe(periods=365)
CSfutureplayer = p.make_future_dataframe(periods=365)
plt.rcParams.update({'figure.figsize':(15,6), 'figure.dpi':120})
forecastr6 = m.predict(R6futureplayer)
forecastcs = p.predict(CSfutureplayer)
m.plot(forecastr6,xlabel='Date',ylabel='Players')
p.plot(forecastcs,xlabel='Date',ylabel='Players')
```
dan akhirnya datapun terplot
![CsGopredict](https://github.com/Bayusatriapersada/Game-Player-Analysis/blob/master/Image/Csgo.PNG)
![r6predict](https://github.com/Bayusatriapersada/Game-Player-Analysis/blob/master/Image/R6.PNG)
