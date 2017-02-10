---
title: Android Temelleri
date: 2014-06-13
author: hamitturkukaya
tags: android, mobile development, java, tr
---

Merhabalar, Java ile Android uygulamaları temelleri hakkında bir giriş yapmak istiyorum. Bunun için işletim sisteminize uygun JDK ve Android SDK' yı indirmeniz gerekmektedir.
Windows ve Mac OSX için JDK ve JRE' yi [buradan](http://www.oracle.com/technetwork/java/javase/downloads/index.html?ssSourceSiteId=otnjp) indirebilirsiniz.

Ubuntu veya Linux Mint için ise:

```
    sudo apt-get install python-software-properties

    sudo add-apt-repository ppa:webupd8team/java

    sudo apt-get update

	sudo apt-get install oracle-java8-installer
```

komutlarını kullanabilirsiniz.

Kurulumun ardından Android SDK' yı ve IDE' mizi indirmemiz gerekmekte. [Buradan](http://developer.android.com/SDK/index.html) Eclipse ile Android SDK' yı indirebiliriz.
İsterseniz Eclipse yerine [IntelliJIdea](http://www.jetbrains.com/idea/) tabanlı [Android Studio](http://developer.android.com/SDK/installing/studio.html)' yu da deneyebilirsiniz,
fakat hala alpha aşamasında olduğu için ben tercih etmiyorum.

## Eclipse

![eclipse](/assets/images/articles/2014-05-09-android-temelleri/eclipse.png)

Eclipse' i açtığımızda sol üstte işaretli 2 ikonumuzu göreceğiz. Bunlardan soldaki Android SDK Manager, yani farklı versiyonlar için Android SDK yüklemeleri yapabileceğimiz kısımdır.
Sağ taraftaki ise Android Virtual Device Manager' dır. Burada da emulatör ile Android bir cihaz oluşturup, testlerimizi onun içinde yapabiliriz.
Fakat maalesef bu araç çok yavaş olduğu için GenyMotion adlı 3. parti emulatörü kullanmanızı öneririm. Standart özellikleri ücretsiz gelmektedir ve standart emülatöre
göre çok daha hızlıdır. (Tabii ki en iyi sonucu gerçek bir cihaz üzerinden alırsınız). GenyMotion' ı [buradan](https://cloud.genymotion.com/page/customer/login/?next=/) üye olduktan sonra
indirebilirsiniz.

## İlk uygulamayı oluşturma

İlk Android uygulamamızı oluşturmak için File > New > Android Application Project seçiyoruz.

![New App](/assets/images/articles/2014-05-09-android-temelleri/newapp.png)

Sonrasında uygulamamız için gerekli bilgileri giriyoruz.

![Naming](/assets/images/articles/2014-05-09-android-temelleri/naming.png)

_**Application name:**_ Play Store' da gözükecek uygulama adıdır

_**Package name:**_ Class' larımızı tutacak genel paket adıdır. Genellikle 'com.sirket_adi.uygulama_adi' olarak belirlenir.

_**Minimum Required SDK**_ ve _**Target SDK**_, uygulamamızın Android' in hangi sürümlerinde çalışacağını belirtir. Target SDK, en son çıkan SDK seçilmelidir.

Sonraki pencerelerde varsayılan değerler korunarak proje oluşturma işlemi tamamlanır.

## Klasörler

![Folders](/assets/images/articles/2014-05-09-android-temelleri/folders.png)

İlk uygulamamızı oluşturduk ve resimdeki gibi klasörler karşımıza geldi. Burada haşır neşir olacağımız kısımlar,
_**SRC**_ ve _**RES**_ klasörleridir. Genel olarak klasörlerin görevleri şunlardır:

_**Gen**_, hiçbir zaman müdahale etmemeniz gereken, Android' in kendi değişkenlerini adresleyip, değişkenler halinde tuttuğu class' ları içeren klasördür.

_**Bin**_, derlenmiş class' larımızı ve çalıştırılabilir apk dosyamızı içeren klasördür.

_**Libs**_, uygulamaya dahil edilen kütüphaneler bu klasördedir. (Android SDK gibi)

_**RES**_, asset' lerimizi tutmak içindir (resimler, arayüz dosyalarımız, rakamsal veya string değerlerimiz vs.)

_**Drawable**_, resimlerimizin, stil dosyalarımızın bulunacağı klasördür. Yanlarındaki hdpi, ldpi, mpdi, xhdpi ise ekran boyutlarını belirtir. Bu şekilde uygulamaya özel arayüz tasarlayabilirsiniz.
Örneğin 10" bir tabletteki resmin boyutu ve çözünürlüğü 3" bir telefondakinden büyük olmalıdır. Bunları burada ayarlayabilirsiniz.

_**Layout**_, arayüz xml' lerini saklayan klasördür. Bu klasörün yanına istediğiniz gibi _layout_hdpi_, _layout_ldpi_ gibi klasörler ekleyerek arayüzleri özelleştirebilirsiniz.

_**Menu**_, uygulamanızda görünecek menüleri tutan klasördür

_**Values**_, uygulama içerisinde kullanacağımız değerleri tutacağımız klasördür. Arayüzdeki margin değerlerinden buton text' lerine kadar herşeyi burada tutabilirsiniz.
values-en, values-tr şeklinde klasörlerle sadece içerisindeki değerleri değiştirerek telefonun diline göre uygulamanın dilini değiştirebilirsiniz.

Bunların dışında içli dışlı olacağımız bir başka dosya, _**AndroidManifest.xml**_ dosyasıdır. Bu dosya içerisinde uygulama ayarlarımız, izinlerimiz, aktivitelerimiz gibi bilgiler
bulunmaktadır.


Bu bilgilerin ardından gelelim layout klasörümüze:

Layout klasörünün içine girdiğimiz zaman 2 adet dosya oluştuğunu görüyoruz. _**activity_main.xml**_ ve _**fragment_main.xml**_ bunlar arayüz dosyalarımızdır.
(Eski SDK' ya sahip olan kullanıcılarda sadece activity_main.xml olacaktır.) Ne işe yaradıklarını açıklayalım. Android' de bir çok ekran sistemi vardır. Bunlara _**Activity**_ denir. Uygulamada işlem
yaptığınız her ekranı bir activity olarak düşünebilirsiniz. Bunun yanısıra API 11(Android 3.0)' den sonra Fragment yapısı ek olarak getirildi. Bunu da Activity içerisinde çalışan bir
arayüz ya da bir işlemi temsil eden küçük activity parçaları olarak düşünebiliriz. Bir container activity içerisinde birden fragment' leri tetikleterek çağırmak, hem performans, hem de
tekrar kullanılabilirlik açısından daha verimlidir. Tabi fragment' ler de activity' den bağımsız değildir. Onların yaşam döngüleri de onu içeren aktiviteye bağlıdır. Activity kapandığı
zaman içerdiği fragment de kapanır.

Bu kısa ön bilgiden sonra tahmin edebileceğiniz gibi activity_main.xml, fragment' i tutacak container activity arayüzü iken; fragment_main.xml ise, içerisinde çalıştırılacak
fragment arayüzüdür.

![Activity](/assets/images/articles/2014-05-09-android-temelleri/newactivity.png)


![Activity](/assets/images/articles/2014-05-09-android-temelleri/newfragment.png)

Layout görünümü içerisinde arayüzü 2 farklı şekilde görüntüleyebiliriz.
_**Graphical Layout**_: Arayüzün olduğu gibi gösterildiği, bileşenlerin sürükle bırak ile eklenebileceği grafik arayüzüdür.
_**XML Editör**_: XML dosyasını manuel olarak oluşturabileceğiniz editördür

Not: Düzenlemeler için xml' e eninde sonunda elle müdahale etmeniz gerekecektir. Arayüz aracı çok gelişmiş durumda değil.

XML dosyalarını arayüz altındaki *activity_main.xml* ve *activity_fragment.xml*' e tıklayarak açalım

_**activity_main.xml**_

```xml
	<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    	xmlns:tools="http://schemas.android.com/tools"
	    android:id="@+id/container"
    	android:layout_width="match_parent"
	    android:layout_height="match_parent"
    	tools:context="com.htk.firstapp.MainActivity"
	    tools:ignore="MergeRootFrame" />
```


Burada, sadece pencere olacağını belirten FrameLayout olarak id' si container olan bir arayüz elementi oluşturulduğunu görüyoruz.
Fragment' imizdeki içerik bu FrameLayout' un içerisine eklenecektir.

_**fragment_main.xml**_

```xml
	<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    	xmlns:tools="http://schemas.android.com/tools"
	    android:layout_width="match_parent"
    	android:layout_height="match_parent"
    	android:paddingBottom="@dimen/activity_vertical_margin"
	    android:paddingLeft="@dimen/activity_horizontal_margin"
    	android:paddingRight="@dimen/activity_horizontal_margin"
	    android:paddingTop="@dimen/activity_vertical_margin"
    	tools:context="com.htk.firstapp.MainActivity$PlaceholderFragment" >

	    <TextView
    	    android:layout_width="wrap_content"
        	android:layout_height="wrap_content"
	        android:text="@string/hello_world" />

	</RelativeLayout>
```

Burada da, içerisinde bir adet TextView bulunan RelativeLayout tanımlanmıştır. Layoutlar içerisinde en çok kullanılan 2 tip layout vardır. Relative ve Linear Layout; isimlerinden de anlaşılabileceği
gibi RelativeLayout, içerisindeki elemanları birbirlerine göre uzaklığı, konumu gibi bilgiler ile yerleşim yaparken, LinearLayout ise, yatay veya dikey olarak elemanları yerleştirir.
Layoutlar iç içe kullanılabilir.

TextView' ımız ise uygulamamızın içerisinde düz metin göstermek için kullanabileceğimiz label' lardır. text değerine _"@string/hello_world"_ değeri atanmıştır. Bu da bu içeriğin
_"res/values/strings.xml"_ dosyası içerisinde tutulduğunu belirtir. Layout içerisindeki yazıları *strings.xml* dosyasında tutmak best practice olarak önerilmektedir.

```xml
	<?xml version="1.0" encoding="utf-8"?>
	<resources>

    	<string name="app_name">FirstApp</string>
    	<string name="hello_world">Hello world!</string>
    	<string name="action_settings">Settings</string>

	</resources>
```

Not: String' ler, id' ler otomatik olarak adreslenip _"Gen/R.class"_ içerisine yazılmaktadır. Bu nedenle aynı string adı ve id' ler farklı xml dosyalarında kullanılsa bile eşsiz olmalıdır.
Mesela yukarıdaki xml' lere bakarak id' si container olan başka bir component veya adı *hello_world* olan başka bir string oluşturmamız hatalara neden olacaktır.

Arayüz dosyalarımızı inceledikten sonra gelelim asıl kodlarımızın bulunduğu Java Class' ımıza.

Class' ımızı _"src/paket_adi/MainActivity.class"_ dosyasına tıklayarak açıyoruz.

```java
    package com.htk.firstapp;

    import android.support.v7.app.ActionBarActivity;
    import android.support.v4.app.Fragment;
    import android.os.Bundle;
    import android.view.LayoutInflater;
    import android.view.Menu;
    import android.view.MenuItem;
    import android.view.View;
    import android.view.ViewGroup;

    public class MainActivity extends ActionBarActivity {

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            if (savedInstanceState == null) {
                getSupportFragmentManager().beginTransaction()
                        .add(R.id.container, new PlaceholderFragment()).commit();
            }
        }

        @Override
        public boolean onCreateOptionsMenu(Menu menu) {

            // Inflate the menu; this adds items to the action bar if it is present.
            getMenuInflater().inflate(R.menu.main, menu);
            return true;
        }

        @Override
        public boolean onOptionsItemSelected(MenuItem item) {
            // Handle action bar item clicks here. The action bar will
            // automatically handle clicks on the Home/Up button, so long
            // as you specify a parent activity in AndroidManifest.xml.
            int id = item.getItemId();
            if (id == R.id.action_settings) {
                return true;
            }
            return super.onOptionsItemSelected(item);
        }

        /**
         * A placeholder fragment containing a simple view.
         */
        public static class PlaceholderFragment extends Fragment {

            public PlaceholderFragment() {
            }

            @Override
            public View onCreateView(LayoutInflater inflater, ViewGroup container,
                    Bundle savedInstanceState) {
                View rootView = inflater.inflate(R.layout.fragment_main, container,
                        false);
                return rootView;
            }
        }
    }
```

Kısaca buradaki eklenmiş fonksiyonların ne iş yaptığını anlatmaya çalışacağım. Görüldüğü gibi MainActivity class' ımız ActionBarActivity' den extend edilmiştir. Bu Activity' nin biraz
daha özelleştirilmiş halidir. Detaylı bilgi ve diğer classları [buradan](http://developer.android.com/reference/android/app/Activity.html) inceleyebirsiniz.

_**onCreateOptionsMenu()**_ menü item' lerin hangi xml dosyasından alınacağını belirten fonksiyondur. (xml dosya ve componentlerin gen/R.class içerisine derlendiğini söylemiştik.
O yüzden R._tip_._ad_ şeklinde çağrılmaktadır).

_**onOptionsItemSelected()**_ menü içerisinden bir seçeneğe tıklandığı zaman tetiklenecek fonksiyondur. Hangi seçeneğe tıklandığı belirlenip gereken işlemler yaptırılabilir.

Gelelim en önemli fonksiyona

_**onCreate**_ fonksiyonu ise activity başlarken çalıştırılacak fonksiyondur. Bu fonksiyon activity yaşam döngüsü (Life Cycle) ile ilgilidir. Bunun yanısıra aşağıdaki fonksiyonları da
ekleyip spesifik işlemler için kullanabilirsiniz.

_**onStart ()**_ : Activity, kullanıcıya görünür hale geldiğinde çağrılır.

_**onResume ()**_ : Activity, kullanıcıyla etkileşime başladığında çağrılır.

_**onPause ()**_ : Mevcut Activity durdurulduğunda ve önceki Activity devam ettirildiğinde çağrılır.

_**onStop ()**_ : Activity, kullanıcıya görünmez hale geldiğinde çağrılır.

_**onDestroy ()**_ : Acitiviy, sistem tarafından yok edilmeden önce çağrılır.

_**onRestart ()**_ : Activity durdurulduğunda ve yeniden başlatıldığında çağrılır.

Bunu da kısaca belirttikten sonra onCreate() fonksiyonunun içeriğini inceleyelim. setContentView() fonksiyonu ile kullanacağı layout dosyasını seçilmektedir. Sonrasında getSupportFragmentManager()
ile fragment yaşam döngüsünü kontrol edebileceğimiz obje alınır. Transaction başlatıp içerisine add fonksiyonu ile fragment class' ımız olan PlaceHolder class' ında tanımlanmış fragment' i çağırmaktadır.
Bu transaction' ı, commit() fonksiyonu ile çalıştırabiliriz.

Fragment Class' ımız olan _**PlaceholderFragment**_' in fonksiyonları da Activity fonksiyonları gibidir. Fragment içerisinde constructordan sonra ilk olarak onCreateView() fonksiyonu
çalıştırılır. Bu fonksiyon içerisinde de fragment layout _**LayoutInflater**_ objesi ile xml dosyamız view nesnesine dönüştürülür. Ardından ise oluşturulan view Activity'e döndürülür ve
activity, bu fragment' i ekrana basar.

Artık temel yapıyı öğrendiğimize göre uygulamamızı çalıştırabiliriz. :)

![First App](/assets/images/articles/2014-05-09-android-temelleri/screenshot.png)
