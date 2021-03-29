# Lab: SQL injection UNION attack, retrieving data from other tables
Bu yazıda, PortSwingger tarafından oluşturulan SQLi lablarının üçüncüsünü inceleyeceğiz.

Lab yönergesi:
This lab contains an SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.

The database contains a different table called users, with columns called username and password.

To solve the lab, perform an SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user.


Sorgudan elde edilen sonuçlar uygulamanın yanıtında döndürülür, böylece diğer tablolardan veri almak için bir UNION saldırısı kullanabilirsiniz.Veritabanı, kullanıcı adı ve parola adı verilen sütunlarla birlikte kullanıcılar adında farklı bir tablo içermektedir. Laboratuvarı çözmek için, tüm kullanıcı adlarını ve şifreleri alan bir SQL injection UNION saldırısı gerçekleştirmemiz ve bilgileri yönetici kullanıcı olarak oturum açmak için kullanmamız istenmektedir. Bunun için Lab1 ve Lab2'deki gibi UNION saldırı tekniklerini kullanacağız ancak sunucunun TABLE kullanıcılarının tüm kullanıcı adlarını ve şifrelerini döndürmesi için bir sorgu ekleyeceğiz.

Sırasıyla aşağıdaki adımları uyguluyoruz:




- Önce bir filtre uygularız ("Aramanızı daraltın" bölümünde belirli bir öğeye tıklayın).
![image](https://user-images.githubusercontent.com/70814577/112760863-28def700-9001-11eb-9d13-000ea9188350.png)
![image](https://user-images.githubusercontent.com/70814577/112760904-51ff8780-9001-11eb-8803-bf5268badfb6.png)

- Sonra, bir sorgu olduğunda döndürülen sütunların sayısını kontrol etmek, burada 'UNION SELECT null, null-- sorgusuyla 2 sütun buluyorum.
![image](https://user-images.githubusercontent.com/70814577/112760936-6f345600-9001-11eb-9f54-c8ce5b0721fd.png)
![image](https://user-images.githubusercontent.com/70814577/112760949-81ae8f80-9001-11eb-83b0-6b3d171e75fe.png)

- Gerçek sütun sayısını öğrendikten sonra, bu sütunların veri türlerini kontrol edeceğiz. 'UNION SELECT' abc ',' xyz '- sorgusuyla 2 optik dize döndürür ve tb bize her iki sütunun da veri türü dizeye sahip olduğunu söyler.
![image](https://user-images.githubusercontent.com/70814577/112760978-9d199a80-9001-11eb-9dbb-6f8a3cd872f3.png)
![image](https://user-images.githubusercontent.com/70814577/112760998-b3275b00-9001-11eb-8bf1-11a57e058f51.png)

Bildiğimiz gibi, kullanıcı adı ve parola da dize türleridir, bu nedenle kullanıcılar tablosundaki kullanıcı adı ve parolayı almak için ekran görüntüsündeki gibi ' UNION SELECT username, password FROM users-- satırını kullanıyoruz.
![image](https://user-images.githubusercontent.com/70814577/112761053-f71a6000-9001-11eb-8386-85f301a3fa76.png)
Sorgunun sonucu olarak sadece yöneticinin şifresini değil, aynı zamanda kullanıcılar tablosunda saklanan tüm kullanıcı adını da aldık. Son olarak, laboratuvarı tamamlamak için giriş yapın ve yöneticinin kullanıcı adını ve şifresini kullanın.
![image](https://user-images.githubusercontent.com/70814577/112761113-3fd21900-9002-11eb-8857-1171f255cd3b.png)
![image](https://user-images.githubusercontent.com/70814577/112761428-f682c900-9003-11eb-9563-9667fc01d5ba.png)
![image](https://user-images.githubusercontent.com/70814577/112761438-04d0e500-9004-11eb-9b9c-0f5440a7b8ed.png)
![image](https://user-images.githubusercontent.com/70814577/112761157-86277800-9002-11eb-8361-3dd98e5f4173.png)
![image](https://user-images.githubusercontent.com/70814577/112761172-9fc8bf80-9002-11eb-9846-d65932de12fb.png)

