# Lab 16

## Өмнөх Лаб11-с өөрчлөгдсөн зүйлс

Frontend-ыг 3000 port дээр, backend-ийг 8080 port дээр proxy-гоор холбосон хөгжүүлэлтийн тохиргооны оронд энэ хэрэгжүүлэлт одоо бүх кодыг backend-ээс 8080 port дээр ажиллуулна. Backend нь frontend-ын хөрвүүлэгдсэн React кодыг / хаягаар хариу боловсруулалт хийдэг бөгөөд серверийн /api хаягууд дээрх API хүсэлтэд хариу өгдөг.

Энэ нь `App.java` файлыг `NanoHTTPD`-ийн оронд `SimpleWebServer`-ээс удамшуулан хийгдсэн бөгөөд `SimpleWebServer` нь статик файлуудыг директороос (конструкторын дуудлагаар тохируулсан директор) боловсруулах аргыг аль хэдийн хэрэгжүүлсэн байдаг. Бид одоо `serve` функцийг `/api` дуудлагад хариу өгөхөөр өөрчилж, бусад бүх хаягийг суперкласс руу шилжүүлсэн. Frontend код нь backend кодтой харьцангуйгаар `../front-end/build` хаяг дээр байх ёстой.

Frontend нь зөвхөн `/api` хаяг дээр API-г хүлээж авахын тулд бага зэрэг өөрчлөгдсөн.

## Суулгалтыг ганц том jar файлаар хийх

Бид `maven-assembly-plugin` plugin-ыг Maven-д ашиглан Java кодыг бүх хамаарлуудын хамт нэг jar файл болгон багцлахдаа `mvn package` командыг дуудахад хэрэглэдэг. Уг файл `target/back-end-1.0-SNAPSHOT-jar-with-dependencies.jar` хаягт байрлана. Pom файлд `configuration/archive/manifest/mainClass` хэсэгт гол классын нэмэлт тодорхойлолт хийснээр одоо хөрвүүлэгдсэн Java кодыг зөвхөн `java -jar target/back-end-1.0-SNAPSHOT-jar-with-dependencies.jar` командаар ажиллуулах боломжтой болсон.

## Бүгдийг build хийх

frontend and the backend-г build хийгээд Docker-той хамт package хийх.

```sh
cd back-end
mvn package
cd ../front-end
npm install
npm run build
cd ..
docker build -t lab13 --platform linux/amd64 .
```

Та контейнерийг `docker run -p 8080:8080 lab13` командаар ажиллуулж болно. Ингэснээр командын мөрөнд сервер эхэлж байгааг харах боломжтой бөгөөд `http://localhost:8080` хаягаар хандах боломжтой байх ёстой.
