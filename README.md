<p align="center">
  <img src="https://github.com/serifaydin/RabbitMQ/blob/master/1.PNG">
</p>
---------
<p align="center">
  <img src="https://github.com/serifaydin/RabbitMQ/blob/master/2.PNG">
</p>
---------
<p align="center">
  <img src="https://github.com/serifaydin/RabbitMQ/blob/master/3.PNG">
</p>


AMQP (Advanced Message Queuing Protocol)
�	Geli�mi� bir mesajla�ma protokol�d�r. 
�	Platform ba��ms�z beberle�me imkan� sunuyor. AMQP destekli bir sunucu var ise, sunucu ile hemen hemen her dil ile Client Ba�lant�s� yaz�labilir.
�	AMQP paketlerinde, header, properties ve message alanlar� bulunur.
AMQP protokol�nde toplam 4 adet exchange tipi var. Direct, Fanout, Topic ve Header. Direct 
AMQP Mesajla�ma Mimarileri
?	Direct Exchange (Point-to-point)
 
?	Bir mesaj �reticisi taraf�ndan (Producer, Publisher) �retilen mesaj�n sadece bir T�keticiye (Consumer) iletildi�i yap�d�r. Birden fazla ayn� i�i yapan t�ketici (Consumer) yaz�lmas�na ra�men, mesaj yaln�zca bir t�ketici (Consumer) taraf�ndan i�lenir. 
?	Mesajlar, mesaj�n �binding key� de�eri ile s�ran�n �routing key� de�erleri aras�nda bir birle�me vard�r. Elimizde hangi mesaj�n hangi s�raya gidece�ini belirleme se�ene�i vard�r.
?	E�er Direct Exchange kullan�rken binding_key ve routing_key belirlenmemi� ise, Direct Exchange Fanout Exchange gibi hareket edip, mesajlar� ili�kide oldu�u t�m s�ralara g�nderecktir.
?	Direct Exchange kullan�rken, Queue olu�turdu�umuzda ki Route Key�i Producer belirtmez ise sistemdeki t�m Direct Exchange Queue lere mesaj eklenecektir.
?	Bir Queue� ye birden fazla Route Key verilir. Publish edilen Route Key� e g�re Queue� ye mesaj g�nderilir.


?	Fanout Exchange (Publish-subscribe)
 
?	Producer� ler taraf�ndan �retilen mesajlar�n, T�m Consumer� lara g�nderildi�i Exchange Type� d�r.
?	Fanout Exchange� e ba�l� t�m Queue lere Producer� den gelen mesaj iletilir. 
?	Fanout Exchange� de Route Key in bir �nemi yoktur.
?	Fanout Exchange� de Producer taraf�ndan bir Queue belirtilmelidir. Yoksa sistem kendisi bir Queue olu�turacakt�r.

?	Topic Exchange
 
Topic Exchange Type; Producer taraf�ndan g�nderilen bir mesaj�n, kurallar g�z �n�nde bulundurularak farkl� Queue lara g�nderilmesi i�leminde kullan�l�r. Kural lar� *. �eklinde belirtebiliyoruz.
A�a��daki �rnek Topik Exchange Route Key kurallar� ile kullan�mlar� belirtilmi�tir.
Kural	Kullan�m�
*.serif	2 kelimeden olu�an 2. Kelimesi serif olan
serif.*	2 kelimeden olu�an 1. Kelimesi serif olan
*.serif.*	3 kelimeden olu�an Ortadaki kelimesi serif olan
serif	Sadece serif olucak

?	Header Exchange
 
RabbitMQ ile Queue olu�turuken, Queue lar�n Header lar�na key-value �eklinde parametreler yazabiliriz. Producer bir Mesaj g�nderdi�inde mesaj�n Properties� inde bulunan header bilgisine g�re, gerekli Queue kuyru�una mesaj eklenecektir.


RabbitMQ
RabbitMQ, bir mesaj kuyru�u sistemidir. Publish ve Subscribe mant��� ile �al���r. RabbitMQ Erlang i�letim sistemi ile yaz�lm��t�r.
�	RabbitMQ bir �ok yaz�l�m diline destek vermektedir.
�	RabbitMQ bir �ok i�letim sistemi ile �al���r.
�	RabbitMQ Open Source dur.
�	RabbitMQ� yu i�letim sistemine kurmadan �nce Erlang dilinin o i�letim sistemine kurulmas� gerekmektedir.
�	RabbitMQ i�erisinde bulundurdu�u Publish, Subscribe ve Routing mekanizmas� ile Geli�mi� Mesaj Kuyru�u Protokol� (AMQP) standard�na uygun olarak �al��maktad�r
�	RabbitMQ Queue� si FIFO (First in First out) ilk giren ilk ��kar, mant���nda �al��maktad�r.
RabbitMQ ile �l�eklenebilir (scakability) bir ortam olu�turabiliriz. Anl�k yap�lmayacak i�lemleri asenkron �ekilde ger�ekle�tirerek;
�	Uygulamalar�m�z� kullanan ki�ileri gereksiz bir response time maliyetinden ar�nd�rm�� oluruz.
�	Server �zerindeki concurrent process maliyetini bir nebze �l�eklenebilir bir hale getirmi� oluruz.
RabbitMQ installer site : http://www.rabbitmq.com/install-windows.html
Erlang installer site : http://www.erlang.org/downloads 
RabbitMQ kullanmak i�in baz� �zel tan�mlar� bilmemiz gerekmektedir.
�	Producer (Publisher) : Kuyru�a mesaj g�nderen uygulamad�r. Mesaj� Exchange� e g�nderir.
�	Consumer : Kuyruktaki mesaj� dinleyecek olan uygulamad�r.
�	Queue : Mesajlar�n RabbitMQ taraf�nda eklendi�i kuyruktur. Exchange� den gelen mesaj� tutar.
�	Exchange : Mesaj� Preducer� den al�r ve Queue� ye g�nderir. Exchange mecburi de�ildir. Bir ka� Exchange tipi bulunmaktad�r. Yapt��� i�lem ise ilgili Routing Key� e g�re mesaj� ilgili Queue� ye y�nlendirmektir.
o	Binding � Exchange i�inde tan�mlanan kurallard�r ve hangi mesaj�n hangi Queue� ye iletilece�ini belirler.
�	Exchange Type : �lgili mesaj� �n Routing Key� e g�re hangi Queue� ye nas�l y�nlendirece�ini belirlemektir. 4 adettir. Direct, Fanout, Headers, Topic Exchange
 
�	Producer: Queue�ya mesaj g�nderen uygulamad�r. Yani Publisher��m�z.
�	Consumer: Queue�daki mesajlar� dinleyecek olan uygulamam�zd�r.
Erlang� i kurduktan sonra, RabbitMQ yu bilgisayar�m�za indirelim ve kural�m. Ard�ndan RabbitMQ Command Prompt� u Administrator Y�netici olarak �al��t�ral�m.
Komut Sat�r� : rabbitmq-plugins enable rabbitmq_management
 
Yukar�daki komut sat�r�n� RabbitMQ Command Prompt� da �al��t�rd���m�zda, yukar�daki resimde de g�r�ld��� �zere Bilgisayar da kurulu olan RabbitMQ servislerini �al��t�r�r.
Erlang ve RabbitMQ kurulumunu ger�ekle�tirdik den sonra. Default olarak http://localhost:15672 adresinden RabbitMW y�netim ekran�n� a�abiliriz.
 
Servis olarak hizmetlerde �al��maktad�r, buradan durdurup veya restart edebiliriz.
 
Windows ba�lat men�s�ne yukar�daki RabbitMQ �zel komutlar� gelecektir.
http://localhost:15672 ile RabbitMQ Dashboard�� �n� a�abiliriz. Fakat girdi�imizde bizi bir Login ekran� kar��layacak default olarak a�a��daki kullan�c� ad� ve �ifre girilmelidir.
�	Kullan�c� Ad� : guest
�	�ifre : guest

RabbitMQ Men�leri ve ��lemleri
 

1.	Overview Men�s�
RabbitMQ server �zerinde ki t�m analiz ve raporlar� buradan canl� olarak takip edebilir gerekirse m�dahale edebiliriz.

2.	Connection Men�s�   
RabbitMQ Server� a ba�l� olan Consumer bilgisini canl� olarak buradan t�m detayl� analiz bilgileri ile ula�abiliriz. 




3.	Channels Men�s�
 
RabbitMQ Server� a ba�l� olan Consumer bilgisini canl� olarak buradan t�m detayl� analiz bilgileri ile ula�abiliriz. Consumer� �n 
�	Virtual host bilgisine ula��labilir. Virtual host
�	Ka� adet mesaj� okudu�u bilgisi burada mevcut. Unacked

4.	Exchanges Men�s�
 
�	RabbitMQ� da 4 adet Exchange tipi vard�r.
�	Bizim de olu�turdu�umuz Exchange Tipleri burada listelenir.
5.	Queues Men�s�
 
RabbitMQ server� da Olu�turulan t�m QUEUE listesine buradan ula��yoruz. Buradan Queue ne durumda ka� adet var k��� i�lendi gibi bir �ok Queue �zelindeki bilgiye rahatl�kla eri�ip y�netebiliyoruz.
�	Ready : �letilecek olan mesaj say�s�
�	Unacked : Consumer lar taf�ndan i�lenen mesaj say�s�
�	Total : Queue i�erisindeki mesaj say�s�.
�	Queue ile ilgili t�m detay bilgilere buradan ula�abiliriz.

6.	RabbitMQ Admin ��lemleri
 
http://localhost:15672/ ad�ndan default olu�an bir host ile RabbitMQ nun t�m s�re�lerini kontrol edebiliyoruz. �u anda kullan�c� i�lemlerini inceleyece�iz.
NOT : RabbitMQ� yu bir server da �al��t�rd���m�zda, farkl� bir lokasyondan veya bilgisayardan guest acount�u ile giri� yapamay�z. Yeni bir Acount olu�turmam�z gerekmektedir.
RabbitMQ� yu farkl� serverlara kurup y�netmek isteyebiliriz. Bunun i�in yapmam�z gereken bir ka� ad�m var.
1.	Add a user sekmesine t�klayal�m ve bir kullan�c� a�al�m.
 



2.	Yukar�daki i�lemin ard�ndan Add user diyelim ve All users sekmesine d�nelim.
 
3.	A��lan kullan�c�ya Virtual Host eklemek i�in, Admin men�s�ndeyken Virtual hosts sekmesine t�klayal�m. 
a.	Default olarak olu�turulan �/� host un i�erisine kullan�c�y� ekleyebiliriz
b.	Add virtual host ile yeni Virtual Host olu�turup kullan�c�y� bu host� a set edebiliriz.
 
4.	Yukar�daki i�lemleri bitirdikten sonra, art�k farkl� lokasyonlardan ve bilgisayardan Server da bulunan RabbitMQ management uygulamas�na eri�ebiliriz. Ayn� zamanda kodlama yapmak i�in bir Connection olu�turmu� olduk.
 
5.	Policies, Limits, Cluster vb. gibi ayarlamalar�da yine Admin penceresi alt�ndan yapabiliriz.
6.	Default olarak gelen �/� Virtual host yerine kendimizde istersek bir Virtusl host olu�turabiliriz.
 
Art�k istedi�imiz takdirde Admin kullan�c�s� arvato Virtusl host� u ile sisteme ba�lanabilir, ve kodlama yapabilir.

RabbitMQ �rnek Kodlar.
Direct Exchange
?	Producer
var rabbitMQService = new RabbitMQService();

            using (var connection = rabbitMQService.GetRabbitMQConnection())
            {
                using (var channel = connection.CreateModel())
                {
                    channel.ExchangeDeclare(CL_ConstModel.ExchangeName, ExchangeType.Direct, true, false, null);

                    //QUEUE CREATED
                    channel.QueueDeclare(CL_ConstModel.queue1Name, true, false, false, null);
                    channel.QueueDeclare(CL_ConstModel.queue2Name, true, false, false, null);
                    channel.QueueBind(CL_ConstModel.queue1Name, CL_ConstModel.ExchangeName, CL_ConstModel.queue1RouteKey);
                    channel.QueueBind(CL_ConstModel.queue2Name, CL_ConstModel.ExchangeName, CL_ConstModel.queue2RouteKey);

                    //QUEUE MESSAGE SEND
                    var publicationAddress = new PublicationAddress(ExchangeType.Direct, CL_ConstModel.ExchangeName, CL_ConstModel.queue1RouteKey);

                    string message = JsonConvert.SerializeObject(UserService.Load());

                    var body = Encoding.UTF8.GetBytes(message);

                    channel.BasicPublish(publicationAddress, null, body);
                }
            }

            Console.WriteLine("Mesaj publish edildi, Direct Exchange' e ba�l� Route Key' e g�re mesaj iletildi 2999.");
            Console.ReadLine();
?	Consumer
Console.WriteLine("Direct Consumer 1");

            var rabbitMQService = new RabbitMQService();

            using (var connection = rabbitMQService.GetRabbitMQConnection())
            {
                using (var channel = connection.CreateModel())
                {
                    var consumer = new EventingBasicConsumer(channel);

                    consumer.Received += (model, ea) =>
                    {
                        index++;
                        var body = ea.Body;
                        var message = Encoding.UTF8.GetString(body);

                        User user = new User();

                        user = JsonConvert.DeserializeObject<User>(message);

                        Console.WriteLine(index + " Queue1 �zerinden mesaj al�nd�: {0} , {1} , {2}", user.Id, user.Name, user.Surname);
                    };

                    channel.BasicConsume(CL_ConstModel.queue1Name, false, consumer);
                    Console.ReadLine();
                }
            }

Fanout Exchange
?	Producer
var rabbitMQService = new RabbitMQService();

            using (var connection = rabbitMQService.GetRabbitMQConnection())
            {
                using (var channel = connection.CreateModel())
                {
                    channel.ExchangeDeclare(CL_ConstModel.ExchangeName, ExchangeType.Fanout, true, false, null);

                    channel.QueueDeclare(CL_ConstModel.queue1Name, true, false, false, null);
                    channel.QueueDeclare(CL_ConstModel.queue2Name, true, false, false, null);

                    channel.QueueBind(CL_ConstModel.queue1Name, CL_ConstModel.ExchangeName, "");
                    channel.QueueBind(CL_ConstModel.queue2Name, CL_ConstModel.ExchangeName, "");

                    var publicationAddress = new PublicationAddress(ExchangeType.Fanout, CL_ConstModel.ExchangeName, "");

                    string message = JsonConvert.SerializeObject(UserService.Load());

                    var body = Encoding.UTF8.GetBytes(message);

                    channel.BasicPublish(publicationAddress, null, body);
                }
            }

            Console.WriteLine("Mesaj publish edildi, Fanout Exchange' e ba�l� t�m Queue lere mesaj iletildi.");
            Console.ReadLine();

?	Consumer
Console.WriteLine("Fanout Consumer 1");
            var rabbitMQService = new RabbitMQService();

            using (var connection = rabbitMQService.GetRabbitMQConnection())
            {
                using (var channel = connection.CreateModel())
                {
                    var consumer = new EventingBasicConsumer(channel);

                    consumer.Received += (model, ea) =>
                    {
                        index++;
                        var body = ea.Body;
                        var message = Encoding.UTF8.GetString(body);
                        User user = JsonConvert.DeserializeObject<User>(message);

                        Console.WriteLine(index + " Queue1 �zerinden mesaj al�nd�: {0} , {1} , {2}", user.Id, user.Name, user.Surname);
                    };

                    channel.BasicConsume(CL_ConstModel.queue1Name, false, consumer);
                    Console.ReadLine();
                }
            }

Header Exchange
?	Producer
var rabbitMQService = new RabbitMQService();

            using (var connection = rabbitMQService.GetRabbitMQConnection())
            {
                using (var channel = connection.CreateModel())
                {
                    channel.ExchangeDeclare(CL_ConstModel.ExchangeName, ExchangeType.Headers, true, false, null);
                    channel.QueueDeclare(CL_ConstModel.queue1Name, true, false, false, null);

                    Dictionary<string, object> headerOptionsWithAll = new Dictionary<string, object>();
                    headerOptionsWithAll.Add("x-match", "all");
                    headerOptionsWithAll.Add("category", "animal");
                    headerOptionsWithAll.Add("type", "mammal");
                    channel.QueueBind(CL_ConstModel.queue1Name, CL_ConstModel.ExchangeName, "", headerOptionsWithAll);

                    //Dictionary<string, object> headerOptionsWithAny = new Dictionary<string, object>();
                    //headerOptionsWithAny.Add("x-match", "any");
                    //headerOptionsWithAny.Add("category", "plant");
                    //headerOptionsWithAny.Add("type", "tree");
                    //channel.QueueBind(CL_ConstModel.queue1Name, CL_ConstModel.ExchangeName, "", headerOptionsWithAny);

                    Dictionary<string, object> messageHeaders = new Dictionary<string, object>();

                    IBasicProperties properties = channel.CreateBasicProperties();
                    messageHeaders = new Dictionary<string, object>();
                    messageHeaders.Add("category", "animal");
                    messageHeaders.Add("type", "mammal");
                    messageHeaders.Add("x-match", "all");
                    properties.Headers = messageHeaders;

                    var publicationAddress = new PublicationAddress(ExchangeType.Headers, CL_ConstModel.ExchangeName, "");
                    string message = JsonConvert.SerializeObject(UserService.Load());
                    var body = Encoding.UTF8.GetBytes(message);
                    channel.BasicPublish(publicationAddress, properties, body);
                }
            }
?	Consumer
Console.WriteLine("Header Consumer 2");

            var rabbitMQService = new RabbitMQService();

            using (var connection = rabbitMQService.GetRabbitMQConnection())
            {
                using (var channel = connection.CreateModel())
                {
                    var consumer = new EventingBasicConsumer(channel);

                    consumer.Received += (model, ea) =>
                    {
                        var body = ea.Body;
                        var message = Encoding.UTF8.GetString(body);
                        User user = JsonConvert.DeserializeObject<User>(message);

                        Console.WriteLine("Queue1 �zerinden mesaj al�nd�: {0} , {1} , {2}", user.Id, user.Name, user.Surname);
                    };

                    channel.BasicConsume(CL_ConstModel.queue2Name, false, consumer);
                    Console.ReadLine();
                }
            }




Topix Exchange
?	Producer
var rabbitMQService = new RabbitMQService();

            using (var connection = rabbitMQService.GetRabbitMQConnection())
            {
                using (var channel = connection.CreateModel())
                {
                    channel.ExchangeDeclare(CL_ConstModel.ExchangeName, ExchangeType.Topic, true, false, null);

                    channel.QueueDeclare(CL_ConstModel.queue1Name, true, false, false, null);
                    channel.QueueDeclare(CL_ConstModel.queue2Name, true, false, false, null);

                    channel.QueueBind(CL_ConstModel.queue1Name, CL_ConstModel.ExchangeName, "*.bmw");
                    channel.QueueBind(CL_ConstModel.queue1Name, CL_ConstModel.ExchangeName, "serif.*");

                    channel.QueueBind(CL_ConstModel.queue2Name, CL_ConstModel.ExchangeName, "merc.*");

                    var publicationAddress = new PublicationAddress(ExchangeType.Headers, CL_ConstModel.ExchangeName, "merc");

                    string message = JsonConvert.SerializeObject(UserService.Load());

                    var body = Encoding.UTF8.GetBytes(message);

                    channel.BasicPublish(publicationAddress, null, body);
                }
            }

?	Consumer
Console.WriteLine("Topic Consumer 1");

            var rabbitMQService = new RabbitMQService();

            using (var connection = rabbitMQService.GetRabbitMQConnection())
            {
                using (var channel = connection.CreateModel())
                {
                    var consumer = new EventingBasicConsumer(channel);

                    consumer.Received += (model, ea) =>
                    {
                        index++;

                        var body = ea.Body;
                        var message = Encoding.UTF8.GetString(body);
                        User user = JsonConvert.DeserializeObject<User>(message);

                        Console.WriteLine(index + " Queue1 �zerinden mesaj al�nd�: {0} , {1} , {2}", user.Id, user.Name, user.Surname);
                    };

                    channel.BasicConsume(CL_ConstModel.queue1Name, false, consumer);
                    Console.ReadLine();
                }
            }



