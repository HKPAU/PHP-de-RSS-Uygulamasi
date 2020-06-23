# PHP-de-RSS-Uygulamasi
<?php
header("Content-Type: text/xmlns");
require_once("baglan.php");

echo "<?xml version='1.0' encoding='UTF-8'?>
<rss xmlns:xsi='https://www.w3.org/2001/XMLSchema-instance' xmlns:xsd='https://www.w3.org/2001/XMLSchema' version='2.0'>
	<channel>
	<title>HKPAU</title>
	<description>Sıfır Urunler</description>
	<link>http://www.hkpau.com</link>
	<language>tr</language>
";

$sorgu 			= $db->query("SELECT * FROM urunler");
$kayitsayisi 	= $sorgu->rowCount();
$kayitlar 		= $sorgu->fetchAll(PDO::FETCH_ASSOC);

foreach ($kayitlar as $value) {
	$urunadi 	= $value["urunadi"];
	$urunfiyati = $value["urunfiyati"];
	$parabirimi = $value["parabirimi"];

	echo "
	<item>
	<title>$urunadi</title>
	<price>$urunfiyati</price>
	<type>$parabirimi</type>
	</item>
	";
}


echo "
	</channel>
</rss>	
";


$db = null;
?>
