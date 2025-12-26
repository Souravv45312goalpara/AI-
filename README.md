<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Voice AI Assistant - Talk to Talk</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: radial-gradient(circle, #001f3f, #000);
            font-family: 'Segoe UI', sans-serif;
        }
        #ui-layer {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-end;
            pointer-events: none;
            padding-bottom: 50px;
        }
        #status-text {
            color: #00ffff;
            font-size: 1.5rem;
            text-shadow: 0 0 15px #00ffff;
            margin-bottom: 10px;
        }
        #subtitles {
            color: white;
            background: rgba(0,0,0,0.5);
            padding: 10px 20px;
            border-radius: 20px;
            font-style: italic;
            max-width: 80%;
            text-align: center;
        }
        .btn-container {
            pointer-events: auto;
            position: absolute;
            top: 20px;
        }
        button {
            padding: 12px 25px;
            cursor: pointer;
            background: #00ffff;
            border: none;
            border-radius: 5px;
            font-weight: bold;
        }
    </style>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

<div class="btn-container">
    <button onclick="startAIAssistant()">ACTIVATE AI VOICE</button>
</div>

<div id="ui-layer">
    <div id="status-text">SYSTEM STANDBY</div>
    <div id="subtitles">Tap 'Activate' to start talking...</div>
</div>

<script>
/* ---------- THREE.JS ---------- */
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });

renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

const geometry = new THREE.SphereGeometry(2, 64, 64);
const material = new THREE.MeshStandardMaterial({
    color: 0x00ffff,
    wireframe: true,
    emissive: 0x00ffff,
    emissiveIntensity: 0.5
});
const orb = new THREE.Mesh(geometry, material);
scene.add(orb);

const light = new THREE.PointLight(0x00ffff, 1, 100);
light.position.set(5, 5, 5);
scene.add(light);

camera.position.z = 6;

let targetScale = 1;

function animate() {
    requestAnimationFrame(animate);

    orb.rotation.y += 0.01;
    orb.rotation.x += 0.005;

    const s = THREE.MathUtils.lerp(orb.scale.x, targetScale, 0.1);
    orb.scale.set(s, s, s);

    renderer.render(scene, camera);
}
animate();

/* ---------- VOICE AI ---------- */
const statusText = document.getElementById("status-text");
const subtitles = document.getElementById("subtitles");

const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
const recognition = new SpeechRecognition();
recognition.continuous = true;
recognition.lang = "en-IN";

const synth = window.speechSynthesis;

function startAIAssistant() {
    recognition.start();
    statusText.innerText = "TALK ME";
    subtitles.innerText = "Say something ";
}

recognition.onresult = (event) => {
    const transcript = event.results[event.results.length - 1][0].transcript.toLowerCase();
    subtitles.innerText = `You: ${transcript}`;
    processAIQuery(transcript);
};

function processAIQuery(query) {
    statusText.innerText = "THINKING...";
    targetScale = 1.5;

    let responseText = "";

    if (query.includes("time")) {
        responseText = `The current time is ${new Date().toLocaleTimeString()}`;
    } else if (query.includes("who are you")) {
        responseText = "I am made by sourav . Another i am AI assistant.";
    }

// Countre
    else if (query.includes("spain")) {
  responseText = "Spain is a Southern European country. It is known for history and festivals.";
}
else if (query.includes("sri lanka")) {
  responseText = "Sri Lanka is an island nation in South Asia. It is famous for tea and beaches.";
}
else if (query.includes("sudan")) {
  responseText = "Sudan is in North Africa. It has a long Nile River history.";
}
else if (query.includes("suriname")) {
  responseText = "Suriname is a small South American country. It has rich rainforests.";
}
else if (query.includes("sweden")) {
  responseText = "Sweden is a Nordic country in Europe. It is known for innovation and nature.";
}
else if (query.includes("switzerland")) {
  responseText = "Switzerland is a European country. It is famous for mountains and banking.";
}
else if (query.includes("syria")) {
  responseText = "Syria is in the Middle East. It has ancient historical cities.";
}
else if (query.includes("taiwan")) {
  responseText = "Taiwan is an island in East Asia. It has a strong technology industry.";
}
else if (query.includes("tajikistan")) {
  responseText = "Tajikistan is in Central Asia. It is mostly mountainous.";
}
else if (query.includes("tanzania")) {
  responseText = "Tanzania is in East Africa. Mount Kilimanjaro is located here.";
}
else if (query.includes("thailand")) {
  responseText = "Thailand is in Southeast Asia. It is known for food and tourism.";
}
else if (query.includes("timor-leste")) {
  responseText = "Timor-Leste is a Southeast Asian nation. It gained independence in 2002.";
}
else if (query.includes("togo")) {
  responseText = "Togo is a West African country. It has a short Atlantic coastline.";
}
else if (query.includes("tonga")) {
  responseText = "Tonga is a Pacific island kingdom. It has strong traditional culture.";
}
else if (query.includes("trinidad and tobago")) {
  responseText = "This Caribbean country has two main islands. It is known for carnival.";
}
else if (query.includes("tunisia")) {
  responseText = "Tunisia is in North Africa. It has Roman and Arab history.";
}
else if (query.includes("turkey")) {
  responseText = "Turkey lies between Europe and Asia. It has rich historical heritage.";
}
else if (query.includes("turkmenistan")) {
  responseText = "Turkmenistan is in Central Asia. It has large desert areas.";
}
else if (query.includes("tuvalu")) {
  responseText = "Tuvalu is a small Pacific island nation. It is threatened by sea level rise.";
}
else if (query.includes("uganda")) {
  responseText = "Uganda is in East Africa. It is known for lakes and wildlife.";
}
else if (query.includes("ukraine")) {
  responseText = "Ukraine is an Eastern European country. It has fertile agricultural land.";
}
else if (query.includes("united arab emirates")) {
  responseText = "UAE is a Middle Eastern country. It is known for modern cities.";
}
else if (query.includes("united kingdom")) {
  responseText = "The UK is in Europe. It has a constitutional monarchy.";
}
else if (query.includes("united states")) {
  responseText = "The USA is in North America. It is a global economic power.";
}
else if (query.includes("uruguay")) {
  responseText = "Uruguay is a South American country. It has a high quality of life.";
}
else if (query.includes("uzbekistan")) {
  responseText = "Uzbekistan is in Central Asia. It was part of the Silk Road.";
}
else if (query.includes("vanuatu")) {
  responseText = "Vanuatu is a Pacific island nation. It has active volcanoes.";
}
else if (query.includes("vatican city")) {
  responseText = "Vatican City is the smallest country in the world. It is the center of Catholicism.";
}
else if (query.includes("venezuela")) {
  responseText = "Venezuela is in South America. It has vast oil reserves.";
}
else if (query.includes("vietnam")) {
  responseText = "Vietnam is in Southeast Asia. It has a long coastal region.";
}
else if (query.includes("yemen")) {
  responseText = "Yemen is in the Middle East. It has ancient trading history.";
}
else if (query.includes("zambia")) {
  responseText = "Zambia is in Southern Africa. Victoria Falls lies on its border.";
}
else if (query.includes("zimbabwe")) {
  responseText = "Zimbabwe is in Southern Africa. It is home to Victoria Falls.";
}
else if (query.includes("kosovo")) {
  responseText = "Kosovo is a Balkan country in Europe. It declared independence in 2008.";
}
else if (query.includes("democratic republic of the congo")) {
  responseText = "DR Congo is in Central Africa. It has vast natural resources.";
}
else if (query.includes("saint helena")) {
  responseText = "Saint Helena is a remote island territory. Napoleon was exiled here.";
}
else if (query.includes("western sahara")) {
  responseText = "Western Sahara is in North Africa. Its status is disputed.";
}
else if (query.includes("oman")) {
  responseText = "Oman is a Middle Eastern country. It has deserts, mountains, and coastline.";
}
else if (query.includes("pakistan")) {
  responseText = "Pakistan is a South Asian country. It has diverse landscapes and cultures.";
}
else if (query.includes("palau")) {
  responseText = "Palau is a Pacific island nation. It is famous for marine life.";
}
else if (query.includes("palestine")) {
  responseText = "Palestine is in the Middle East. It has deep historical significance.";
}
else if (query.includes("panama")) {
  responseText = "Panama is in Central America. The Panama Canal is located here.";
}
else if (query.includes("papua new guinea")) {
  responseText = "Papua New Guinea is in Oceania. It has rich tribal cultures.";
}
else if (query.includes("paraguay")) {
  responseText = "Paraguay is a landlocked South American country. It has strong cultural traditions.";
}
else if (query.includes("peru")) {
  responseText = "Peru is in South America. It is home to Machu Picchu.";
}
else if (query.includes("philippines")) {
  responseText = "Philippines is an island country in Southeast Asia. It has thousands of islands.";
}
else if (query.includes("poland")) {
  responseText = "Poland is a Central European country. It has a long and complex history.";
}
else if (query.includes("portugal")) {
  responseText = "Portugal is in Southern Europe. It has a long Atlantic coastline.";
}
else if (query.includes("qatar")) {
  responseText = "Qatar is a Middle Eastern country. It is rich in natural gas.";
}
else if (query.includes("romania")) {
  responseText = "Romania is an Eastern European country. It is known for the Carpathian Mountains.";
}
else if (query.includes("russia")) {
  responseText = "Russia is the largest country in the world. It spans Europe and Asia.";
}
else if (query.includes("rwanda")) {
  responseText = "Rwanda is an East African country. It is known as the land of a thousand hills.";
}
else if (query.includes("saint kitts and nevis")) {
  responseText = "Saint Kitts and Nevis is a Caribbean nation. It consists of two islands.";
}
else if (query.includes("saint lucia")) {
  responseText = "Saint Lucia is a Caribbean island country. It is famous for the Pitons.";
}
else if (query.includes("saint vincent and the grenadines")) {
  responseText = "This is a Caribbean island nation. It is known for sailing and beaches.";
}
else if (query.includes("samoa")) {
  responseText = "Samoa is a Pacific island country. It has strong Polynesian culture.";
}
else if (query.includes("san marino")) {
  responseText = "San Marino is a small European country. It is one of the oldest republics.";
}
else if (query.includes("sao tome and principe")) {
  responseText = "São Tomé and Príncipe is an island nation in Africa. It lies in the Gulf of Guinea.";
}
else if (query.includes("saudi arabia")) {
  responseText = "Saudi Arabia is a Middle Eastern country. It is the birthplace of Islam.";
}
else if (query.includes("senegal")) {
  responseText = "Senegal is a West African country. It is known for music and culture.";
}
else if (query.includes("serbia")) {
  responseText = "Serbia is a Balkan country in Europe. It has rich historical heritage.";
}
else if (query.includes("seychelles")) {
  responseText = "Seychelles is an island nation in the Indian Ocean. It is famous for beaches.";
}
else if (query.includes("sierra leone")) {
  responseText = "Sierra Leone is a West African country. It has beautiful coastal areas.";
}
else if (query.includes("singapore")) {
  responseText = "Singapore is a city-state in Southeast Asia. It is a global financial hub.";
}
else if (query.includes("slovakia")) {
  responseText = "Slovakia is a Central European country. It has mountainous regions.";
}
else if (query.includes("slovenia")) {
  responseText = "Slovenia is a small European nation. It has Alps and Adriatic coast.";
}
else if (query.includes("solomon islands")) {
  responseText = "Solomon Islands is a Pacific nation. It consists of many islands.";
}
else if (query.includes("somalia")) {
  responseText = "Somalia is in East Africa. It has a long Indian Ocean coastline.";
}
else if (query.includes("south africa")) {
  responseText = "South Africa is in Southern Africa. It has diverse cultures and wildlife.";
}
else if (query.includes("south korea")) {
  responseText = "South Korea is in East Asia. It is known for technology and pop culture.";
}
else if (query.includes("south sudan")) {
  responseText = "South Sudan is the youngest country in the world. It is in East Africa.";
}
else if (query.includes("laos")) {
  responseText = "Laos is a landlocked country in Southeast Asia. It is known for mountains and rivers.";
}
else if (query.includes("latvia")) {
  responseText = "Latvia is a Baltic country in Europe. It has a long Baltic Sea coastline.";
}
else if (query.includes("lebanon")) {
  responseText = "Lebanon is a Middle Eastern country. It has a rich cultural history.";
}
else if (query.includes("lesotho")) {
  responseText = "Lesotho is a landlocked country in Africa. It is surrounded by South Africa.";
}
else if (query.includes("liberia")) {
  responseText = "Liberia is a West African country. It was founded by freed slaves.";
}
else if (query.includes("libya")) {
  responseText = "Libya is in North Africa. Much of it is desert land.";
}
else if (query.includes("liechtenstein")) {
  responseText = "Liechtenstein is a small European country. It lies between Austria and Switzerland.";
}
else if (query.includes("lithuania")) {
  responseText = "Lithuania is a Baltic country. It has a strong historical identity.";
}
else if (query.includes("luxembourg")) {
  responseText = "Luxembourg is a small European nation. It has a strong financial sector.";
}
else if (query.includes("madagascar")) {
  responseText = "Madagascar is an island nation in Africa. It has unique wildlife.";
}
else if (query.includes("malawi")) {
  responseText = "Malawi is in Southeast Africa. Lake Malawi is a major feature.";
}
else if (query.includes("malaysia")) {
  responseText = "Malaysia is in Southeast Asia. It has modern cities and rainforests.";
}
else if (query.includes("maldives")) {
  responseText = "Maldives is an island country in the Indian Ocean. It is famous for beaches.";
}
else if (query.includes("mali")) {
  responseText = "Mali is a West African country. It has ancient trade history.";
}
else if (query.includes("malta")) {
  responseText = "Malta is a small island nation in Europe. It has ancient temples.";
}
else if (query.includes("marshall islands")) {
  responseText = "Marshall Islands is a Pacific nation. It consists of many atolls.";
}
else if (query.includes("mauritania")) {
  responseText = "Mauritania is in West Africa. Much of it is desert.";
}
else if (query.includes("mauritius")) {
  responseText = "Mauritius is an island nation in the Indian Ocean. Tourism is important.";
}
else if (query.includes("mexico")) {
  responseText = "Mexico is in North America. It has ancient civilizations and culture.";
}
else if (query.includes("micronesia")) {
  responseText = "Micronesia is a Pacific island nation. It consists of many small islands.";
}
else if (query.includes("moldova")) {
  responseText = "Moldova is a European country. It is known for wine production.";
}
else if (query.includes("monaco")) {
  responseText = "Monaco is a small European city-state. It is famous for luxury.";
}
else if (query.includes("mongolia")) {
  responseText = "Mongolia is in East Asia. It has vast grasslands and nomadic culture.";
}
else if (query.includes("montenegro")) {
  responseText = "Montenegro is a Balkan country. It has a scenic Adriatic coast.";
}
else if (query.includes("morocco")) {
  responseText = "Morocco is in North Africa. It has strong Arab and Berber culture.";
}
else if (query.includes("mozambique")) {
  responseText = "Mozambique is in Southeast Africa. It has a long Indian Ocean coastline.";
}
else if (query.includes("myanmar")) {
  responseText = "Myanmar is in Southeast Asia. It has ancient temples and culture.";
}
else if (query.includes("namibia")) {
  responseText = "Namibia is in Southern Africa. It is known for deserts and wildlife.";
}
else if (query.includes("nauru")) {
  responseText = "Nauru is a tiny Pacific island country. It is one of the smallest nations.";
}
else if (query.includes("nepal")) {
  responseText = "Nepal is a Himalayan country. Mount Everest lies there.";
}
else if (query.includes("netherlands")) {
  responseText = "Netherlands is a European country. It is famous for canals and bicycles.";
}
else if (query.includes("new zealand")) {
  responseText = "New Zealand is an island nation in the Pacific. It has beautiful landscapes.";
}
else if (query.includes("nicaragua")) {
  responseText = "Nicaragua is in Central America. It has lakes and volcanoes.";
}
else if (query.includes("niger")) {
  responseText = "Niger is a West African country. Much of it is Sahara desert.";
}
else if (query.includes("nigeria")) {
  responseText = "Nigeria is in West Africa. It has the largest population in Africa.";
}
else if (query.includes("north korea")) {
  responseText = "North Korea is in East Asia. It is a highly isolated country.";
}
else if (query.includes("north macedonia")) {
  responseText = "North Macedonia is a Balkan country. It has rich ancient history.";
}
else if (query.includes("norway")) {
  responseText = "Norway is a Nordic country. It is famous for fjords.";
}
else if (query.includes("denmark")) {
  responseText = "Denmark is a Nordic country in Europe. It is known for high quality of life.";
}
else if (query.includes("djibouti")) {
  responseText = "Djibouti is in East Africa. It has a strategic port location.";
}
else if (query.includes("dominica")) {
  responseText = "Dominica is a Caribbean island nation. It is rich in natural forests.";
}
else if (query.includes("dominican republic")) {
  responseText = "The Dominican Republic is in the Caribbean. Tourism is a major industry.";
}
else if (query.includes("ecuador")) {
  responseText = "Ecuador is in South America. The Galápagos Islands belong to it.";
}
else if (query.includes("egypt")) {
  responseText = "Egypt is in North Africa. It is famous for ancient pyramids.";
}
else if (query.includes("el salvador")) {
  responseText = "El Salvador is in Central America. It is the smallest country there.";
}
else if (query.includes("equatorial guinea")) {
  responseText = "Equatorial Guinea is in Central Africa. It has oil resources.";
}
else if (query.includes("eritrea")) {
  responseText = "Eritrea is in East Africa. It has a long Red Sea coastline.";
}
else if (query.includes("estonia")) {
  responseText = "Estonia is a Baltic country in Europe. It is advanced in digital services.";
}
else if (query.includes("eswatini")) {
  responseText = "Eswatini is a small African kingdom. It was formerly called Swaziland.";
}
else if (query.includes("ethiopia")) {
  responseText = "Ethiopia is in East Africa. It has an ancient civilization.";
}
else if (query.includes("fiji")) {
  responseText = "Fiji is an island nation in the Pacific. It is known for coral reefs.";
}
else if (query.includes("finland")) {
  responseText = "Finland is a Nordic country. It is famous for education and lakes.";
}
else if (query.includes("france")) {
  responseText = "France is a European country. It is known for art and fashion.";
}
else if (query.includes("gabon")) {
  responseText = "Gabon is in Central Africa. It has dense rainforests.";
}
else if (query.includes("gambia")) {
  responseText = "The Gambia is a small West African country. It follows the Gambia River.";
}
else if (query.includes("georgia")) {
  responseText = "Georgia lies between Europe and Asia. It has a rich cultural history.";
}
else if (query.includes("germany")) {
  responseText = "Germany is in Central Europe. It has a strong industrial economy.";
}
else if (query.includes("ghana")) {
  responseText = "Ghana is a West African country. It was the first to gain independence there.";
}
else if (query.includes("greece")) {
  responseText = "Greece is in Southern Europe. It is known as the birthplace of democracy.";
}
else if (query.includes("grenada")) {
  responseText = "Grenada is a Caribbean island nation. It is called the Spice Island.";
}
else if (query.includes("guatemala")) {
  responseText = "Guatemala is in Central America. It has strong Mayan heritage.";
}
else if (query.includes("guinea")) {
  responseText = "Guinea is a West African country. It has rich mineral resources.";
}
else if (query.includes("guinea-bissau")) {
  responseText = "Guinea-Bissau is in West Africa. It has many coastal islands.";
}
else if (query.includes("guyana")) {
  responseText = "Guyana is in South America. English is its official language.";
}
else if (query.includes("haiti")) {
  responseText = "Haiti is a Caribbean nation. It shares an island with the Dominican Republic.";
}
else if (query.includes("honduras")) {
  responseText = "Honduras is in Central America. It has Caribbean coastline.";
}
else if (query.includes("hungary")) {
  responseText = "Hungary is a Central European country. Budapest is its capital.";
}
else if (query.includes("iceland")) {
  responseText = "Iceland is a Nordic island nation. It has volcanoes and geysers.";
}
else if (query.includes("indonesia")) {
  responseText = "Indonesia is an island country in Southeast Asia. It has thousands of islands.";
}
else if (query.includes("iran")) {
  responseText = "Iran is in the Middle East. It has a long Persian history.";
}
else if (query.includes("iraq")) {
  responseText = "Iraq is in the Middle East. It is home to ancient Mesopotamia.";
}
else if (query.includes("ireland")) {
  responseText = "Ireland is an island nation in Europe. It is known for green landscapes.";
}
else if (query.includes("israel")) {
  responseText = "Israel is in the Middle East. It has historical and religious importance.";
}
else if (query.includes("italy")) {
  responseText = "Italy is in Southern Europe. It is famous for art and cuisine.";
}
else if (query.includes("jamaica")) {
  responseText = "Jamaica is a Caribbean island nation. It is known for reggae music.";
}
else if (query.includes("jordan")) {
  responseText = "Jordan is a Middle Eastern country. Petra is a famous landmark.";
}
else if (query.includes("kazakhstan")) {
  responseText = "Kazakhstan is in Central Asia. It is the largest landlocked country.";
}
else if (query.includes("kenya")) {
  responseText = "Kenya is in East Africa. It is famous for wildlife safaris.";
}
else if (query.includes("kiribati")) {
  responseText = "Kiribati is a Pacific island nation. It lies near the equator.";
}
else if (query.includes("kuwait")) {
  responseText = "Kuwait is a Middle Eastern country. It has vast oil reserves.";
}
else if (query.includes("kyrgyzstan")) {
  responseText = "Kyrgyzstan is in Central Asia. It has mountainous landscapes.";
}
else if (query.includes("afghanistan")) {
  responseText = "Afghanistan is a landlocked country in South Asia. It has a rich ancient history.";
}
else if (query.includes("albania")) {
  responseText = "Albania is a country in Southeast Europe. It lies along the Adriatic Sea.";
}
else if (query.includes("algeria")) {
  responseText = "Algeria is the largest country in Africa. Much of it is covered by the Sahara Desert.";
}
else if (query.includes("andorra")) {
  responseText = "Andorra is a small country between France and Spain. It is famous for mountains.";
}
else if (query.includes("angola")) {
  responseText = "Angola is a country in Southern Africa. It is rich in oil and minerals.";
}
else if (query.includes("antigua and barbuda")) {
  responseText = "Antigua and Barbuda is a Caribbean island nation. It is known for beaches.";
}
else if (query.includes("argentina")) {
  responseText = "Argentina is in South America. It is famous for tango and football.";
}
else if (query.includes("armenia")) {
  responseText = "Armenia is a country in the Caucasus region. It has ancient Christian heritage.";
}
else if (query.includes("australia")) {
  responseText = "Australia is both a country and a continent. It is known for wildlife.";
}
else if (query.includes("austria")) {
  responseText = "Austria is a European country. It is famous for music and the Alps.";
}
else if (query.includes("azerbaijan")) {
  responseText = "Azerbaijan lies between Europe and Asia. It is rich in oil and gas.";
}
else if (query.includes("bahamas")) {
  responseText = "The Bahamas is an island country in the Atlantic. Tourism is its main industry.";
}
else if (query.includes("bahrain")) {
  responseText = "Bahrain is a small Middle Eastern island nation. It is a financial hub.";
}
else if (query.includes("bangladesh")) {
  responseText = "Bangladesh is in South Asia. It is known for rivers and textiles.";
}
else if (query.includes("barbados")) {
  responseText = "Barbados is a Caribbean island nation. It has a strong cultural heritage.";
}
else if (query.includes("belarus")) {
  responseText = "Belarus is an Eastern European country. It has vast forests and lakes.";
}
else if (query.includes("belgium")) {
  responseText = "Belgium is in Western Europe. It is famous for chocolates and waffles.";
}
else if (query.includes("belize")) {
  responseText = "Belize is in Central America. It has coral reefs and rainforests.";
}
else if (query.includes("benin")) {
  responseText = "Benin is a West African country. It has historical ties to ancient kingdoms.";
}
else if (query.includes("bhutan")) {
  responseText = "Bhutan is a Himalayan country. It measures progress by happiness.";
}
else if (query.includes("bolivia")) {
  responseText = "Bolivia is a landlocked South American country. It has diverse geography.";
}
else if (query.includes("brazil")) {
  responseText = "Brazil is the largest country in South America. It hosts the Amazon rainforest.";
}
else if (query.includes("brunei")) {
  responseText = "Brunei is a small Southeast Asian nation. It is very rich in oil.";
}
else if (query.includes("bulgaria")) {
  responseText = "Bulgaria is a Balkan country. It has a long cultural history.";
}
else if (query.includes("burkina faso")) {
  responseText = "Burkina Faso is in West Africa. It is known for traditional music.";
}
else if (query.includes("burundi")) {
  responseText = "Burundi is a small African nation. It lies near Lake Tanganyika.";
}
else if (query.includes("cambodia")) {
  responseText = "Cambodia is in Southeast Asia. Angkor Wat is located here.";
}
else if (query.includes("cameroon")) {
  responseText = "Cameroon is in Central Africa. It has diverse cultures and landscapes.";
}
else if (query.includes("canada")) {
  responseText = "Canada is in North America. It has vast land and cold climate.";
}
else if (query.includes("chile")) {
  responseText = "Chile is a long country in South America. It stretches along the Pacific.";
}
else if (query.includes("china")) {
  responseText = "China is in East Asia. It has the largest population in the world.";
}
else if (query.includes("colombia")) {
  responseText = "Colombia is in South America. It is famous for coffee production.";
}
else if (query.includes("costa rica")) {
  responseText = "Costa Rica is in Central America. It is known for biodiversity.";
}
else if (query.includes("croatia")) {
  responseText = "Croatia is a European country. It has a beautiful Adriatic coast.";
}
else if (query.includes("cuba")) {
  responseText = "Cuba is a Caribbean island nation. It is known for music and culture.";
}
else if (query.includes("cyprus")) {
  responseText = "Cyprus is an island in the Mediterranean. It has ancient history.";
}
else if (query.includes("czech republic")) {
  responseText = "Czech Republic is in Central Europe. Prague is its capital city.";
}
else if (query.includes("india")) {
  responseText = "India is a South Asian country. It has diverse cultures and languages.";
}
else if (query.includes("japan")) {
  responseText = "Japan is an island country in East Asia. It blends tradition and technology.";
}
else if (query.includes("germany")) {
  responseText = "Germany is in Europe. It has a strong economy and history.";
}
else if (query.includes("france")) {
  responseText = "France is a Western European country. It is famous for art and cuisine.";
}
else if (query.includes("russia")) {
  responseText = "Russia is the largest country in the world. It spans Europe and Asia.";
}
else if (query.includes("united kingdom")) {
  responseText = "The UK is in Europe. It includes England, Scotland, Wales, and Northern Ireland.";
}
else if (query.includes("united states")) {
  responseText = "The USA is in North America. It is a global economic power.";
}
else if (query.includes("vatican city")) {
  responseText = "Vatican City is the smallest country. It is the center of the Catholic Church.";
}
else if (query.includes("taiwan")) {
  responseText = "Taiwan is an island in East Asia. It has a strong tech industry.";
}
else if (query.includes("zimbabwe")) {
  responseText = "Zimbabwe is a Southern African country. It is home to Victoria Falls.";
}






//ASSAM
else if (query.includes("what is assam")) {
  responseText = "Assam is a state in Northeast India. It is known for tea, rivers, and culture.";
}
else if (query.includes("where is assam located")) {
  responseText = "Assam is located in Northeast India. It lies along the Brahmaputra River.";
}
else if (query.includes("capital of assam")) {
  responseText = "Dispur is the capital of Assam. It is part of Guwahati city.";
}
else if (query.includes("largest city of assam")) {
  responseText = "Guwahati is the largest city of Assam. It is the gateway to Northeast India.";
}
else if (query.includes("main language of assam")) {
  responseText = "Assamese is the main language of Assam. It is an Indo-Aryan language.";
}
else if (query.includes("other languages spoken in assam")) {
  responseText = "Bodo, Bengali, Hindi, and English are also spoken in Assam.";
}
else if (query.includes("people of assam called")) {
  responseText = "People of Assam are called Assamese. They belong to many ethnic groups.";
}
else if (query.includes("main river of assam")) {
  responseText = "The Brahmaputra is the main river of Assam. It is one of the longest rivers in Asia.";
}
else if (query.includes("why assam is famous")) {
  responseText = "Assam is famous for tea, wildlife, and silk. It has rich cultural heritage.";
}
else if (query.includes("assam tea")) {
  responseText = "Assam produces world-famous tea. It is known for strong flavor.";
}

else if (query.includes("famous festival of assam")) {
  responseText = "Bihu is the most famous festival of Assam. It celebrates harvest and culture.";
}
else if (query.includes("how many bihu in assam")) {
  responseText = "There are three Bihu festivals. Rongali, Kongali, and Bhogali Bihu.";
}
else if (query.includes("traditional dress of assam")) {
  responseText = "Mekhela Chador is traditional dress for women. Men wear Dhoti and Gamosa.";
}
else if (query.includes("what is gamosa")) {
  responseText = "Gamosa is a traditional cloth of Assam. It symbolizes respect and pride.";
}
else if (query.includes("traditional food of assam")) {
  responseText = "Rice, fish, and bamboo shoot are common foods. Assamese cuisine is simple.";
}
else if (query.includes("famous sweet of assam")) {
  responseText = "Pitha is a famous Assamese sweet. It is made during Bihu.";
}
else if (query.includes("assam silk")) {
  responseText = "Assam is famous for Muga silk. It is unique and golden in color.";
}
else if (query.includes("assam wildlife")) {
  responseText = "Assam has rich wildlife. It has national parks and forests.";
}
else if (query.includes("kaziranga national park")) {
  responseText = "Kaziranga is famous for one-horned rhinoceros. It is a UNESCO site.";
}
else if (query.includes("manas national park")) {
  responseText = "Manas is a national park in Assam. It is known for biodiversity.";
}

else if (query.includes("assam culture")) {
  responseText = "Assamese culture is diverse and ancient. It includes music, dance, and festivals.";
}
else if (query.includes("assam dance")) {
  responseText = "Bihu dance is the most popular dance. It is energetic and joyful.";
}
else if (query.includes("assam music")) {
  responseText = "Assamese music includes folk and modern styles. Zubeen Garg is very famous.";
}
else if (query.includes("famous singer of assam")) {
  responseText = "Zubeen Garg is one of the most famous singers of Assam.";
}
else if (query.includes("assam literature")) {
  responseText = "Assam has rich literature. Sankardev played a major role.";
}
else if (query.includes("sankardev")) {
  responseText = "Srimanta Sankardev was a great saint and reformer. He shaped Assamese culture.";
}
else if (query.includes("assam history")) {
  responseText = "Assam has ancient history. The Ahom dynasty ruled for 600 years.";
}
else if (query.includes("ahom dynasty")) {
  responseText = "The Ahoms ruled Assam for centuries. They protected Assam from invasions.";
}
else if (query.includes("assam freedom fighters")) {
  responseText = "Assam had many freedom fighters. They contributed to India’s independence.";
}

else if (query.includes("assam climate")) {
  responseText = "Assam has humid climate. It receives heavy rainfall.";
}
else if (query.includes("flood in assam")) {
  responseText = "Floods are common in Assam. The Brahmaputra causes seasonal flooding.";
}
else if (query.includes("assam economy")) {
  responseText = "Assam’s economy depends on agriculture, tea, and oil.";
}
else if (query.includes("assam oil")) {
  responseText = "Assam is the first oil-producing state in India. Digboi is famous for oil.";
}
else if (query.includes("digboi oil refinery")) {
  responseText = "Digboi has Asia’s oldest oil refinery. It is located in Assam.";
}

else if (query.includes("assam education")) {
  responseText = "Assam has universities and colleges. Guwahati University is well known.";
}
else if (query.includes("assam tourism")) {
  responseText = "Tourism in Assam includes wildlife, temples, and rivers.";
}
else if (query.includes("kamakhya temple")) {
  responseText = "Kamakhya Temple is a famous Shakti Peeth. It is in Guwahati.";
}
else if (query.includes("majuli island")) {
  responseText = "Majuli is the world’s largest river island. It is in Assam.";
}
else if (query.includes("assam border")) {
  responseText = "Assam shares borders with many states and countries.";
}

else if (query.includes("assam people nature")) {
  responseText = "Assamese people are known to be polite and hospitable.";
}
else if (query.includes("assam tribal people")) {
  responseText = "Assam has many tribal communities. Each has unique culture.";
}
else if (query.includes("bodo people")) {
  responseText = "Bodos are a major ethnic group in Assam. They have their own language.";
}
else if (query.includes("assam unity")) {
  responseText = "Assam shows unity in diversity. Many cultures live together.";
}
else if (query.includes("assam traditional games")) {
  responseText = "Traditional games include buffalo fighting and boat racing.";
}
else if (query.includes("assam modern lifestyle")) {
  responseText = "Modern Assam blends tradition and technology. Cities are developing fast.";
}

else if (query.includes("is assam safe")) {
  responseText = "Assam is generally safe. People are friendly to visitors.";
}
else if (query.includes("assam youth")) {
  responseText = "Assamese youth are talented and creative. Many work in arts and sports.";
}
else if (query.includes("assam sports")) {
  responseText = "Football is very popular in Assam. Many young players are emerging.";
}
else if (query.includes("assam internet")) {
  responseText = "Internet usage is growing in Assam. Digital services are expanding.";
}
else if (query.includes("assam future")) {
  responseText = "Assam has a bright future. Development and culture are growing together.";
}


    else if (query.includes("your name")) {
        responseText = "My name is Voice AI Assistant.";
    }
    else if (query.includes("weather")) {
        responseText = "I cannot fetch live weather data right now, but it's always a good idea to check a weather app!";
    }
    else if (query.includes("thank you")) {
        responseText = "You're welcome! Happy to help.";
    }
    else if (query.includes("exit") || query.includes("stop")) {
        responseText = "Shutting down. Goodbye!";
        recognition.stop();
        statusText.innerText = "SYSTEM STANDBY";
    }
    else if (query.includes("hello") || query.includes("hi")) {
        responseText = "Hello! How can I assist you today?";
    }
    else if (query.includes("how are you")) {
        responseText = "I'm just a program, but thanks for asking!";
    }

    else    if (query.includes("joke")) {
        responseText = "Why did the scarecrow win an award? Because he was outstanding in his field!";
    }

    else if (query.includes("motivate me")) {
        responseText = "Believe in yourself! Every great achievement starts with the decision to try.";
    }
    else if (query.includes("date") || query.includes("day")) {
        const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
        responseText = `Today is ${new Date().toLocaleDateString(undefined, options)}`;
    }
    else if (query.includes("Who made you") || query.includes("who created you")) {
        responseText = "Sourav made me.";
    }
    else if (query.includes("open google")) {
        responseText = "Opening Google for you.";
        window.open("https://www.google.com", "_blank");
    }
     else if (query.includes("open youtube")) {
        responseText = "Opening YouTube for you.";
        window.open("https://www.youtube.com", "_blank");
    }
     else if (query.includes("open facebook")) {
        responseText = "Opening Facebook for you.";
        window.open("https://www.facebook.com", "_blank");
    }
     else if (query.includes("open instagram")) {
        responseText = "Opening Instagram for you.";
        window.open("https://www.instagram.com", "_blank");
    }
     else if (query.includes("open twitter")) {
        responseText = "Opening Twitter for you.";
        window.open("https://www.twitter.com", "_blank");
    }
     else if (query.includes("open whatsapp")) {
        responseText = "Opening WhatsApp for you.";
        window.open("https://web.whatsapp.com", "_blank");
    }
     else if (query.includes("open gmail")) {
        responseText = "Opening Gmail for you.";
        window.open("https://mail.google.com", "_blank");
    }
     else if (query.includes("open netflix")) {
        responseText = "Opening Netflix for you.";
        window.open("https://www.netflix.com", "_blank");
    }
     else if (query.includes("open amazon")) {
        responseText = "Opening Amazon for you.";
        window.open("https://www.amazon.com", "_blank");
    }
     else if (query.includes("open ebay")) {
        responseText = "Opening eBay for you.";
        window.open("https://www.ebay.com", "_blank");
    }
     else if (query.includes("open linkedin")) {
        responseText = "Opening LinkedIn for you.";
        window.open("https://www.linkedin.com", "_blank");
    }
    else if (query.includes("open github")) {
        responseText = "Opening GitHub for you.";
        window.open("https://www.github.com", "_blank");
    }
    else if (query.includes("open stack overflow")) {
        responseText = "Opening Stack Overflow for you.";
        window.open("https://stackoverflow.com", "_blank");
    }
    else if (query.includes("open reddit")) {
        responseText = "Opening Reddit for you.";
        window.open("https://www.reddit.com", "_blank");
    }
    else if (query.includes("open wikipedia")) {
        responseText = "Opening Wikipedia for you.";
        window.open("https://www.wikipedia.org", "_blank");
    }
    else if (query.includes("open cnn")) {
        responseText = "Opening CNN for you.";
        window.open("https://www.cnn.com", "_blank");
    }
    else if (query.includes("open bbc")) {
        responseText = "Opening BBC for you.";
        window.open("https://www.bbc.com", "_blank");
    }
    else if (query.includes("open nytimes") || query.includes("open new york times")) {
        responseText = "Opening The New York Times for you.";
        window.open("https://www.nytimes.com", "_blank");
    }
    else if (query.includes("open hulu")) {
        responseText = "Opening Hulu for you.";
        window.open("https://www.hulu.com", "_blank");
    }
    else if (query.includes("open disney plus") || query.includes("open disney+")) {
        responseText = "Opening Disney Plus for you.";
        window.open("https://www.disneyplus.com", "_blank");
    }
    else if (query.includes("open spotify")) {
        responseText = "Opening Spotify for you.";
        window.open("https://www.spotify.com", "_blank");
    }
    else if (query.includes("open apple music")) {
        responseText = "Opening Apple Music for you.";
        window.open("https://music.apple.com", "_blank");
    }
    else if (query.includes("open soundcloud")) {
        responseText = "Opening SoundCloud for you.";
        window.open("https://www.soundcloud.com", "_blank");
    }
    else if (query.includes("open twitch")) {
        responseText = "Opening Twitch for you.";
        window.open("https://www.twitch.tv", "_blank");
    }
    else if (query.includes("who Zubeen garg")) {
        responseText = "Zubeen Garg (1972-2025) was a legendary Indian singer, composer, actor, and multi-talented artist from Assam, celebrated for his prolific work in Assamese, Bengali, and Hindi music, known for hits like 'Ya Ali' and for his immense contribution to regional culture as a cultural icon, philanthropist, and outspoken activist, who passed away in September 2025";
    }
    else {
        responseText = "I heard you. Please continue.";
    }
    speak(responseText);
}

function speak(text) {
    recognition.stop();

    const utterance = new SpeechSynthesisUtterance(text);

    utterance.onstart = () => {
        statusText.innerText = "AI TALKING...";
        targetScale = 2.0;
    };

    utterance.onend = () => {
        statusText.innerText = "LISTENING...";
        targetScale = 1.0;
        recognition.start();
    };

    const voices = synth.getVoices();
    utterance.voice = voices.find(v => v.lang.includes("en")) || voices[0];

    subtitles.innerText = `AI: ${text}`;
    synth.speak(utterance);
}
</script>

</body>
</html># AI-
