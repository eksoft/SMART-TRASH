# SMART-TRASH
Proje Konusu : Akıllı Çöp Kutusu (Smart Trash Can) 
 
Proje Açıklaması : Projemiz ülkemizin her yanında bulunan çöp kutularının merkezi bir birimden kontrolünü sağlayarak zaman, maliyet ve iş gücünden tasarruf etmeyi hedeflemektedir. 
 
Proje Detayları : Projemiz içerisinde bir çok teknolojiyi barındıran bir IOT projesidir. Kullanılan teknolojiler ; firebase , Arduino uno-Wemos D1 , ASP.NET MVC . 
  
Firebase : Bu teknoloji çöp kutumuzda bulunan sensörün ürettiği verileri gerçek zamanlı olarak depolamamızı sağlayan teknolojidir. Google tarafından desteklenen bir yapıdır.  
Arduino uno-Wemos D1: Bu modül çöp kutusuna yerleştirdiğimiz sensörlerin bağlı olduğu mikro denetleyicidir. Sensörlerin okuduğu veriyi inernet ortamındaki sunucuya aktarmamız için internet bağlantısını sağlayan bir wifi modülüdür.  
ASP.NET MVC : Çöp kutumuzdan üretilen verilerin firebase’e aktarımından sonra bu verileri işleyip anlamlı hale getirdiğimiz kısımdır. Anlamlı halden kasıt çöp kutusunun kaç saatte dolduğu , hangi saatlerde boş olduğu ve çöp kamyonu için en kısa yolu çıkarabilmektir.  
 
Projemizin çalışma mekanizması çöp kutusuna yerleştirdiğimiz mikro denetleyici aracılığıyla gerçekleşir. Mikro denetleyicimize bağlı olan sensörler aracılığıyla bazı verilerin ölçümü yapılır (uzaklık, sıvı , ağırlık). Bu elde edilen veriler wifi modülümüz aracılığıyla internete bağlanarak firebase veritabanına kaydedilir . Veri tabanımızda çöp kutumuzun güncel hali tutulur. Ardından bu verileri kullanarak merkezi birime toplanması gereken çöplerin bulunduğu en kısa yol haritası web arayüzünden aktarılır.  
 
Projemizin faydalarını yukarıda belirtmiştik . Çıkardığımız en kısa yol haritası sayesinde , boş olan çöp kutularına gitmeyerek zamandan ve iş gücünden tasarruf sağlıyor. Yine bu sayede çöp kamyonlarının gereksiz yerlere gitmesini engelleyerek yakıttan tasarruf sağlıyor. Bu tasarruflar sadece yakıt ve zaman bazlı düşünmemek gerekir , aynı zamanda boş yere harcanan iş gücüde minimuma indirgenmiş oluyor.  
 
Projenin Gerçeklenmesi 
Yakınlık Sensörünün Kullanılması 
Konum bazlı olarak çöp konteynırlarındaki doluluk oranını ölçen projemizde; yakınlık sensörü olarak HC-SR04 kullanıldı. Sensörün çalışma şekli ses dalgalarının cisme gönderilip geri gelmesi sayeside gerçekleşmekte. Ses dalgası cisme çarpıp geri geldiği için ölçülen mesafenin 2’ye bölümünden kalan sonuç ses hızına bölünerek cm cinsinden mesafe elde etmiş olduk. 
Firebase bağlantısının yapılması ve Web ortamına aktarılması 
Firebase’deki verilerin web sitesine aktarılması işlemi için ise öncelikle Firebase konsoluna giriş yapıldı, ardından “Add Firebase to your web app” seçeneği seçilerek bir javascript kodu elde edildi.Elde edilen örnek kod ve içeriği aşağıdaki gibidir. 
 
<script 
  src="https://www.gstatic.com/firebasejs/5.7.0/firebase.js">
</script>
<script>   
// Initialize Firebase  
// TODO: Replace with your project's customized code snippet
var config = {    
  apiKey: "<API_KEY>", 
  authDomain: "<PROJECT_ID>.firebaseapp.com",  
  databaseURL: "https://<DATABASE_NAME>.firebaseio.com", 
  projectId: "<PROJECT_ID>",   
  storageBucket: "<BUCKET>.appspot.com",   
  messagingSenderId: "<SENDER_ID>",  
};   
firebase.initializeApp(config); 
</script> 
 
Firebase bağlantısını sağladıktan sonra “distance” değerini 3 saniyede bir okuyarak bar yardımıyla yüzdesel olarak karşılığını gösterdik. Diğer yandan eğer ölçülen mesafe konteynırın derinliğinden fazlaysa kapağın açık olduğu uyarısını verdirdik ve barın rengini kırmızı olarak değiştirdik. 
