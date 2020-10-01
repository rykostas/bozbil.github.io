---
layout: post
title: Basitçe Accuracy, Precision, Recall ve F1 Score
subtitle: Bir sınıflandırma probleminin/işleminin ne kadar başarılı olduğunu anlamak için çeşitli değerlendirme kriterleriyle sonuçlarımızı analiz etmemiz gerekir. Bu yazıda en basit şekilde bu kriterler nelerdir ve nasıl kullanılırlar sorularına ışık tutacağız.
cover-img: https://www.vectorsecurity.com/userfiles/images/bus%20blog/bus-shoplifter2-lrg.jpg
tags: [Machine Learning,Evaluation,Accuracy,F1 Score]
comments: true
---



# Basitçe Accuracy, Precision, Recall ve F1 Score

### Bir sınıflandırma probleminin/işleminin ne kadar başarılı olduğunu anlamak için çeşitli değerlendirme kriterleriyle sonuçlarımızı analiz etmemiz gerekir. Bu yazıda en basit şekilde bu kriterler nelerdir ve nasıl kullanılırlar sorularına ışık tutacağız.





Her şeyden önce problemimizi belirleyelim/yaratalım:

Hayali bir markete güvenlik şefi olarak alınmak üzere başvurduğunuzu düşünün. Marketin sahibi size, mahallede hırsızlık oranlarının çok yüksek olduğunu bunun için sezgileri kuvvetli birini aradıklarını söyleyerek bir uygulama yapmanızı istiyor. Bu işlem sonucunda sizin ne kadar başarılı olduğunuz gözlemlenecek. Uygulama şöyle:

Marketten çıkan 10 müşterinin hırsız olup olmadığını tahmin edeceksiniz. Bu Tahmin verilerini oluşturacak. Market çıkışında bu 10 müşterinin hepsinin üstü aranacak ve hırsız olup olmadıklarına bakılarak Gerçek veriler oluşturulacak. Daha sonra bu iki veri kıyaslanarak sizin ne kadar başarılı olduğunuz aanaliz edilecek.

Aşağıdaki resimde (Şekil 1)Gerçek ve Tahmin verilerini görüyorsunuz. Kırmız renk hırsızı, siyah ise normal müşteriyi gösteriyor.


![cmd](https://miro.medium.com/max/1240/1*QmYVsvEhcN1CMf8xqDskgg.png)
<sub><sup>         Şekil 1- Tahmin ve Gerçek verilerin görselleştirilmesi (kırmızı: hırsız, siyah:normal).</sup></sub>

Şekil 1 incelenirse bazı tahminlerimizde başarılı bazılarında ise başarısız olduğumuzu görürüz. Bu tahminleri 4 grup altında toplayabiliriz. Bunlar :

**TP**: Eğer bir kişiye hırsız dediniz ve o kişi hırsızsa **True Positive**.

**TN**: Eğer bir kişiye hırsız değil dediniz ve o kişi hırsız değilse **True Negative**.

**FP**: Eğer bir kişiye hırsız dediniz ve o kişi hırsız değilse **False Positive**.

**FN**: Eğer bir kişiye hırsız değil dediniz ve o kişi hırsızsa **False Negative**.

![cmd](https://miro.medium.com/max/1400/1*9xoUazA-Ghv3K2iOvbLRvw.png)
<sub><sup>         Şekil 2- TP, TN, FP ve FN kavramlarının görselleştirilmesi.</sup></sub>

Bu dört grubu, bir arada gösteren tabloya confusion matrix (Hata Matrisi) diyoruz. Tahminlerimizin confusion matrix üzerindeki dağılımını Şekil 3'de görebilirsiniz. Şekil ürerindeki sari daireler tahmin edilen müşterilerin numaralarını gösterir.


![cmd](https://miro.medium.com/max/1400/1*wXOW5qTZMWIgwC_9WiFFlg.png )
<sub><sup> Şekil 3- Tahminlerimizin confusion matrix üzerindeki dağılımı</sup></sub>


Değerlendirme yöntemleri arasında en yaygın olarak kullanılan yöntem, **Accuracy (Doğruluk)**’ dur.


**Accuracy** tüm doğru cevaplarınızın(TP), tüm cevaplarınıza (TP,TN,FP,FN) oranı olarak kısaca açıklanabilir ( TP/(TP+TN+FP+FN)). Sık kullanılmasına rağmen accuracy’nin bir dezavantajı vardır: dengesiz dağılıma sahip gruplarda sağlıklı sonuç vermez.


şöyle bir örnekle açıklayalım: yine markette hırsızlığı tespit etmeye çalıştığımızı farzedelim. İnsanların pek azı hırsızdır. Diyelim ki çalınan ürünleri tespit eden bir alarm sistemimiz var ve ne yazık ki sistemimiz bozuk. 100 kişilik müşterilerimiz içerisinde yalnızca bir hırsız olsun. Sitemimiz bozuk olduğu için bu kişiyi tespit edemedik ancak günün sonunda başarımızı ağer accuracy ile ölçersek (Şekil 4'ü inceleyin):

![cmd](https://miro.medium.com/max/1400/1*3NSDQLa6MJWqwDQ9WVGRVA.png )
<sub><sup> Şekil 4 — Örnek için yaratılan confusion matrix ve Accuracy’nin hesaplaması</sup></sub>



işlemin sonucunda %99 oranında başarılı olduğumuz görülür. Aslında hiç fena değil :)
Sistemimiz tamamen arızalı iken bile %99 başarı oranı sağlıyor ki bu tamamen yanıltıcı ve hiç istediğimiz bir şey değil.

İşte tam olarak bu yüzden accuracy dışında da çeşitli değerlendirme yöntemleri kullanılmaktadır. Bunlar şu şekilde tanımlanabilir:

**Recall (Duyarlılık/Hassasiyet)**: doğru tespit ettiğimiz Pozitif sınıfların (TP, doğru tahmin ettiğimiz hırsızlar), Tüm pozitiflere oranı (bizim doğru tahmin etmemizden bağımsız olarak gerçekten hırsız olanlar, yani TP+FN). Şekil 5, İlk hücre bölü ilk sütun (TP/(TP+FN)).

![cmd](https://miro.medium.com/max/1400/1*6x1aLVFtaeoor8Ak2XFbkQ.png)
<sub><sup> Şekil 5- Örnek confusion matrix </sup></sub>

**Precision (Kesinlik) **: doğru tespit ettiğimiz Pozitif sınıfların (TP, doğru tahmin ettiğimiz hırsızlar) tüm hırsız diye etiketlediğimiz/adlandırdığımız verilere oranı (TP+FP). Başka bir değişle bildiğimiz hırsızların sayısının, bildiğimiz hırsızlar ve yanlış alarmların toplamına oranı. Şekil 5, İlk hücre bölü ilk satır (TP/(TP+FP))


Burada precision/ recall arasındaki dengeden de bahsetmek gerekir. Yaptığınız işe göre precision/ recall arasında tercih yapmanız gerekebilir. 

Ek örnekle açıklayalım:
Market örneğinde, bazen hırsızların çaldıkları şeyleri çok iyi sarıp sarmaladıklarında, cihazımızı kandırabildiklerini düşünelim. Marketteki alarmımızın bir hassasiyet ayarı olsun, eğer bu ayarı yükseltirsek, sarıp sarmalanan cihazları da yakalıyor (gerçek hırsızlar yakalanıyor / TP artıyor). Ancak, bunun bir dezavantajı var, bu alarm bazen üzerinde çeşitli metal eşya taşıyan normal müşteriler için de ötüyor (yanlış alarmlar — FP yükseliyor). Yaptığımız ayar neticesinde, TP oranını yükselttik, FN sayısında bir değişiklik olmadı bu yüzden Recall değerimiz yükselmeye başladı. Diğer taraftan yaptığımız bu hassas ayar yanlış alarm sayısını yükselttiği için Precision değerimiz düşmeye başladı.

**Başka bir deyişle sistemimizin hassasiyetini (Recall)arttırmamız kesinlik (Precision) değerimizin düşmesine neden olabilir**. Burada önemli olan şey sisteminizin öncelikleridir. Önceliklerinizi analiz ederek bu dengeyi iyi ayarlamanız gerekir.


Accuracy’ye alternatif olabilecek bir başka değerlendirme yöntemi ise **F1 Score**’dur. F1 Score’un dengesiz dağılıma sahip verisetleri için kullanımı daha doğru olacaktır.


![cmd](https://miro.medium.com/max/1400/1*6k0DZYRQ23sV4tHiSGfP8A.png)
<sub><sup> F1 Score Formülü</sup></sub>


F1 Score, Precision ve Recall’un harmonik ortalamasıdır. Harmonik ortalamanın normal ortalamadan farkı, taraf güçsüzün yanında olmasıdır 😊. F1, yüksek değeri cezalandırır, böylece bu iki değerden yüksek olan düşük olanı manipüle etmesinin önüne geçer . Harmonik ortalama ve normal ortalamanın farkını sezmek için aşağıdaki tabloyu inceleyebilirsiniz.


![cmd](https://miro.medium.com/max/1400/1*af6_SHR6jPJtMTjbo0IjQw.png)
<sub><sup>harmonik ortalama vs normal ortalama</sup></sub>


<div class="fb-comments" data-href="https://bozbil.github.io/" data-numposts="4" data-width=""></div>
