### 1- NE: 
#### Liskov's Subsitute Principle Nedir ?
Liskov's Subsitute Principle SOLID prensiplerinden bir tanesidir.

Liskov prensibine göre; kalıtım bozulmamalı, üst sınıf ile miras alan 
alt sınıf arasında davranış olarak hiçbir fark olmamalıdır. Yani birbirlerinin yerine kullanılabilmelidirler.

Bu yer değiştirme durumunda, sınıfa özel bir istisna kesinlikle oluşmamalıdır. Miras alınan sınıftaki her bir method, 
özellik miras alan alt sınıfta kullanılmalıdır. Eğer bir alt sınıf bu işlevlerden herhangi birini kullanmıyor ise
Liskov'un bu prensibine aykırı bir durum söz konusudur. 

### 2- NEDEN:
#### Liskov's Subsitute Principle Kullanım Amacı ?
Bu prensibe göre bir sınıfın alt sınıfları 
kullanılmak için ekstra bir efor gerektirmemelidir. 
Alt sınıflarda meydana gelen davranış değişiklikleri, 
bu metotların hatalı çalışmasına sebep verebilir. 
Bu tip hatalı çalışmaların önüne geçmek için davranış değişikliği olan 
her sınıfta değişiklik yapılması gerekmektedir. 
Bu da ekstra çaba harcanarak her yeni sınıf için bu tip davranış değişikliklerinin kontrol edilmesi anlamına gelir.

### 3- NASIL:
#### Liskov's Subsitute Principle Nasıl Kullanılır ?
Liskov'un prensibine uygun bir uygulama ortaya koymak için alt sınıflarda 
değişiklik gösterecek işlevleri ana sınıftan miras alacak şekilde ayrı alt sınıflara bölebiliriz. Böylelikle yeni 
oluşacak alt sınıflar ihtiyaclarına göre bu sınıfları miras alarak kullansın ve kullanmayacakları işlevlerin sınıflarını 
miras almasın. Bu şekilde Liskov'un prensibine uygun bir uygulama ortaya çıkmış olur.

#### Örnek:
Kuşları tanımlayıp üzerinde işlem yapacağımız ve miras alınacak sınıf Bird sınıfı olsun ve bu sınıfı içerisinde 2 adet 
method bulunsun, eat() ve fly(). 
Bu ana methoddan miras alarak oluşacak kuş alt sınıfları da Pigeon ve Chicken olsun.
Baktığımız zaman hem pigeon, yani güvercin, hem de chicken, yani tavuk, eat() methodunu yerine getirirken.
fly() methodunu ise pigeon yerine getirir fakat chicken yerine getiremez, çünkü tavuklar uçamaz.

Liskov'un prensibine göre miras alındıkları Bird sınıfındaki methodları çalıştırmaları gerekmekte. Ya da başka bir deyişle
oluşturulan alt sınıflardan herhangi biri için istisna yapılamaz. Bu durumda mevcut şartlar Liskov prensibine uygun değil.

Bu sebeple bu methodları ayrı sınıflara bölüp oluşacak Pigeaon ve Chicken alt sınıflarını bu sınıflardan miras aldırmalıyız.

***Liskov'a Aykırı Durum:***

```
public class Bird {

    public void eat() {
        System.out.println("I can eat.");
    }

    public void fly() {
        System.out.println("I can fly.");
    }
}
public class Pigeon extends Bird {}
public class Chicken extends Bird {}
```

***Liskov'a Uygun Durum:***

```
public class Bird {

    public void eat() {
        System.out.println("I can eat.");
    }

}
public class FlyingBird extends Bird {

    public void fly() {
        System.out.println("I can fly.");
    }
}
public class Pigeon extends FlyingBird {}
public class Chicken extends Bird {}
```
*fly()* methodunu ana sınıftan ayırdık ve FlyingBird adında Bird sınıfından miras alan yeni bir sınıf oluşturduk ki
Pigeon hem bu sınıftan miras alarak *fly()* methodunu çalıştırabilsin , hem de bu FlyingBird sınıfının miras aldığı Bird 
sınıfının *eat()* methodunu çalıştırsın. Bu arada Chicken da Bird methodundan miras aldığı için *eat()* methodunu çalıştırırken
ihtiyacı olmayan *fly()* metoduyla bağını kesmiş oldu.
