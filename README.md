# myob-mini-opdracht 2.0

Hoe laad je een stylesheet in? 
Het inladen van een stylesheet in WordPress kan door het in de header.php te zetten. Alleen als best practice is er een andere manier. Hoe zou jij dit doen zodat bijvoorbeeld versie beheer voor caching ook wordt meegenomen?

**Stylesheet Antwoord** 
Open FTP-client (met bijvoorbeeld FileZilla) en login op je FTP omgeving. Ga naar functions.php (meestal: public_html > wp-content > themes > jouw child theme naam > function.php en download dit bestand.
Open dit bestand in je code editor.
Plaats onderstaande code onderin je functions.php en upload je functions.php weer.

function enqueue_my_custom_styles() {
  // Registreer mijn custom stylesheet
  wp_register_style( 'custom-styles', get_stylesheet_directory_uri() . '/css/custom.css' );
  // Laad mijn custom stylesheet
  wp_enqueue_style( 'custom-styles' );
}

add_action( 'wp_enqueue_scripts', 'enqueue_my_custom_styles', 99 );

Het enige wat we nu nog moeten doen is in je child-theme een map aan te maken genaamd CSS en daarin je custom.css bestand te plaatsen.

**Omgaan met data**
WordPress get_posts is een handige functie waarmee je content uit de WordPress-database kunnen ophalen. Je kunt op gedetailleerd niveau aangeven naar welke berichten, pagina’s en aangepaste berichtentypes je op zoek bent, je eigen set aan resultaten krijgen en vervolgens de items filteren en ordenen.

Naar mijn idee krijg je met onderstaande code de laatste 5 blog berichten te zien... :

$args = array(
	'numberposts'	=> 5,
);
$my_posts = get_posts( $args );

if( ! empty( $my_posts ) ){
	$output = '<ul>';
	foreach ( $my_posts as $p ){
		$output .= '<li><a href="' . get_permalink( $p->ID ) . '">' 
		. $p->post_title . '</a></li>';
	}
	$output .= '<ul>';
} 



Wat houdt ‘the_loop’ in en waarom gebruiken we dit?
Data binnen the standaard WordPress omgeving zit binnen the_loop. Hoe gebruik je dit en welke data is er op te vragen in dit ontwerp patroon van WordPress?

Antwoord: 
Een Wordpress thema geeft alleen nog statische inhoud weer. Wordpress heeft een speciale methode om de pagina's dynamisch te maken. Dat wil zeggen dat met een bepaald bestand, bijvoorbeeld index.php, pagina's met verschillende inhoud kunnen worden weergegeven. Deze speciale methode wordt 'The Loop' genoemd. 
Het query loop blok is een editor om content op je website weer te geven. Met behulp van filteropties kun je de weergegeven content beperken op basis van -Categorieën -Tags -Auteur -Trefwoorden.
Het query Loop blok bevat een aantal subblokken om je nog meer controle te geven over hoe je content exact wordt weegegeven. De volgende blokken kunnen worden toegevoegd aan het query Loop blok. -Berichttitel -Berichtdatum -Berichtinhoud -Samenvatting bericht -Afbeelding met bericht -Berichtcategorieën -Berichttags -Vorige en volgende bericht. 


**Plugin gebruik**
Wat is het juiste moment om een plugin te gebruiken en wanneer wil je deze updaten? 

Ter verduidelijking een scenario: een klant heeft een autowas bedrijf, hiervoor wilt de procesmanager een website met hierop een planningsfunctionaliteit. Gaan we dit van scratch schrijven of downloaden / kopen we een plugin? Wat zijn de voor en/of nadelen van het gebruik van een externe plugin en waarom wil je deze updaten (mits mogelijk)?

Antwoord: 
Als er voor een functionaliteit veel code moet worden geschreven kun je om het werk te vergemakkelijken een plugin gebruiken. 
Als je zelf code hebt geschreven, moet je dit ook handmatig moet onderhouden. Het kan voorkomen dat het op een gegeven moment niet meer compatibel is met de huidige Wordpress versie. Het gebruik van plugins levert tijdwinst op.
Er kleven ook nadelen aan plugins :
-Plugins kunnen zorgen voor een tragere website
-Verouderde pluginversies zijn een potentieel gevaar voor een hack
-Plugins kunnen conflicteren met elkaar
-Plugins kunnen niet compatibel zijn met de website
-Bij gebruik van veel plugins kan het updaten een enorme taak worden

Wanneer je ervoor kiest om op zoek te gaan naar een plugin moet je letten op een aantal facetten:
-Compatibiliteit: is deeze plugin compatibel met de huidige versie van Wordpress?
-Aantal installaties: Hoe vaker de plugin geïnstalleerd is hoe beter.
-Laatste Update: wanneer is de plugin voor het laatst bijgewerkt? Wanneer dit te lang geleden is kun je ervan uitgaan dat de security van de plugin te   wensen overlaat.

Wanneer is een plugin overbodig :
-Kleine aanpassingen
-Overbodige functies
-Net niet plugin

Hierbij hoop ik voldoende antwoorden te hebben gegeven op de vragen. 
Groet! Jeske


