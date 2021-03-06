
Not : Türkçe dökümantasyon aşağıdadır.

See [Change Log](Changelog.md)


# Turkish NLP with Python

## Performance 

**System : Processor : 1,6 GHz Intel Core i5 , RAM : 8 GB 1600 MHZ DDR3 , Macbook Air

|  Method    | Execution Time (ms) | Words Count|
|------------|----------|----------|
| auto_correct                     | 135 ms                  | 1000 words |
| is_turkish                       | 1 ms                    | 1000 words |
| syllabicate_sentence             | 94 ms                   | 1000 words |


Very early version of the TurkishNLP. For now it has basically 5 main functions; Detecting Turkish Language, correcting typos, vowel harmonic detection, Turkish origin detection and syllabication in Turkish words.

## Dataset
Dataset was created by parsing and filtering a Turkish wikipedia dump. 

## Getting Started
To get started first you need to install the package. With using pip;
```
pip install turkishnlp
```
And you can install the most recent version by;
```
pip install --upgrade turkishnlp
```
After installing the package succesfully try and import the package.

```
import turkishnlp
```
### Downloading the data
To download the data first we need to create an instance of TurkishNLP class. So we need to ;
```
from turkishnlp import detector
obj = detector.TurkishNLP()
```
After creating the instance we can simply call the download function like this;

```
obj.download()
```
It will take shortly and after the download it will print out "Download succesful". You won't have to download the data again.

### Creating the wordset
To create the wordset from data you need to ;
```
obj.create_word_set()
```
And it will create the wordset and necesary dictionaries.

### Example Usage
So there are 5 main functions, detecting if the language is Turkish, Turkish typo correction, vowel harmony detection, Turkish origin detection and syllabication.

### Language Detection
```
print(obj.is_turkish("Ben bugün ankaraya gideceğim belki birşeyler alırım"))
```
Will return us "True" along with the accuracy point which is 0.85

### Typo Correction

```
lwords = obj.list_words("vri kümsi idrae edre ancaka daha güezl oalbilir")
print(obj.auto_correct(lwords))
```
Which will print out ['veri', 'kümesi', 'idare', 'eder', 'ancak', 'daha', 'güzel', 'olabilir']. "List_words" method simply splits the text by words with the help of regex. You can simply use "join" to make it a sentence again like this;

```
lwords = obj.list_words("vri kümsi idrae edre ancaka daha güezl oalbilir")
corrected_words = obj.auto_correct(lwords)
corrected_string = " ".join(corrected_words)
```
Which will print out 'veri kümesi idare eder ancak daha güzel olabilir'. 

### Syllabication

```
obj.syllabicate_sentence("Hiç unutmadım, doğudan esen hafif bir yel saçlarını dalgalandırıyordu")
```
And it will give you ;

"[['hiç'], ['u', 'nut', 'ma', 'dım,'], ['do', 'ğu', 'dan'], ['e', 'sen'], ['ha', 'fif'], ['bir'], ['yel'], ['saç', 'la', 'rı', 'nı'], ['dal', 'ga', 'lan', 'dı', 'rı', 'yor', 'du']]"

### Vowel Harmony

This is a Turkish language rule. You can check if a word is vowel harmonic by doing this;


```
obj.is_vowel_harmonic("Belki")
```
Which will return True, since it is vowel harmonic.

### Is Turkish Origin

Again there are Turkish language rules so you can check if a word is Turkish origin or not. For example;
The word 'program' is not a Turkish word. Lets try and check;

```
obj.is_turkish_origin("program")
```
Returns false. On the other hand the word 'yazılım';

```
obj.is_turkish_origin("yazılım")
```
Gives us True

# Python ile Türkçe Dil İşleme

TurkishNLP kütüphanesinin alfa versiyonu. Şimdilik Türkçe dilini tespit etme, Türkçe yazım hatalarını düzeltme, büyük ünlü uyumu kontrolü, Türkçe köken kontrolü ve kelimeleri hecelere ayrıma olmak üzere 5 ana fonksiyonu var

## Veri
Veri kümesi wikipedia'nın Türkçe dump'ı parselanıp temizlenerek oluşturuldu.

## Başlarken
Öncelikle başlamadan, pip ile kütüphaneyi yüklemeniz gerekiyor. Şu şekilde;
```
pip install turkishnlp
```
Ayrıca şu şekilde yayınlanan son versiyonu indirebilirsiniz;
```
pip install --upgrade turkishnlp
```
Yükledikten sonra kütüphaneyi şu şekilde import etmeyi deneyin;

```
import turkishnlp
```
### Veriyi indirmek
Veriyi indirmek için önce TurkishNLP sınıfından türetilmiş bir obje oluşturmamız lazım;
```
from turkishnlp import detector
obj = detector.TurkishNLP()
```
Objeyi oluşturduktan sonra indirme metodunu şu şekilde çağırarak indirme işlemini başlatabiliriz ;

```
obj.download()
```
İndirme işlemi çok uzun sürmeden bitecek ve ardından "Download Succesful" yani indirme başarılı manasına gelen bir yazı ekrana basılacak

### Verisetini oluşturmak
İndirdiğimiz veriden kodun içinde kullanacağımız verisetlerini oluşturmak için basitce;
```
obj.create_word_set()
```
Yapıyoruz ve işlem tamamlanmış oluyor

### Örnek Kullanım
Başlıkta da belirttiğim gibi temel olarak 5 metod var.

### Türkçe Dil Tespiti

```
print(obj.is_turkish("Ben bugün ankaraya gideceğim belki birşeyler alırım"))
```
Yaptığında göreceğiz ki, ekrana "True" bastırıyor ve doğruluk oranı olarak 0.85 döndürüyor.

### Yazım Hatası Düzeltme

```
lwords = obj.list_words("vri kümsi idrae edre ancaka daha güezl oalbilir")
print(obj.auto_correct(lwords))
```
Yapıyoruz ve sonuç olarak bize ['veri', 'kümesi', 'idare', 'eder', 'ancak', 'daha', 'güzel', 'olabilir'] listesi veriliyor. Burada "list_words" metodunun yaptığı string olarak gelen texti regex yardımıyla kelimelerine ayırmaktır Kelimeleri birleştirmek için Python'ın "join" metodu kullanılabilir. Örneğin;

```
lwords = obj.list_words("vri kümsi idrae edre ancaka daha güezl oalbilir")
corrected_words = obj.auto_correct(lwords)
corrected_string = " ".join(corrected_words)
```
Yazdıracağı sonuç : 'veri kümesi idare eder ancak daha güzel olabilir'. 

### Hecelere Ayırmak 
```
obj.syllabicate_sentence("Hiç unutmadım, doğudan esen hafif bir yel saçlarını dalgalandırıyordu")
```
Yapıyoruz. Ve dönen sonuç;

"[['hiç'], ['u', 'nut', 'ma', 'dım,'], ['do', 'ğu', 'dan'], ['e', 'sen'], ['ha', 'fif'], ['bir'], ['yel'], ['saç', 'la', 'rı', 'nı'], ['dal', 'ga', 'lan', 'dı', 'rı', 'yor', 'du']]"

### Büyük Ünlü Uyumu

Herhangi bir kelimenin büyük ünlü uyumuna uyup uymadığını şu şekilde kontrol edebiliriz;

```
obj.is_vowel_harmonic("Belki")
```
'belki' kelimesi büyük ünlü uyumuna uyduğundan bu işlem bize True döndürecektir

### Türkçe Köken Kontrolü

Bir kelimenin Türkçe kökenli olup olmadığını öğrenmek için çeşitli kurallar var. turkishnlp kütüphanesiyle 'program' kelimesinin türkçe kökenli olup olmadığını öğrenmek için;

```
obj.is_turkish_origin("program")
```
Yapıyoruz ve bize False değeri döndürüyor. Öte yandan 'yazılım' kelimesi için

```
obj.is_turkish_origin("yazılım")
```
Yapıyoruz ve bize True değerini döndürüyor
