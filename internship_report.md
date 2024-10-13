Day 1: Setting Up the Development Environment

İlk gün, geliştirme ortamını kurarken XAMPP ve Docker'ı yüklemekle geçti. Apache sunucusunun nasıl yapılandırıldığını öğrenmek için temel bir PHP sayfası oluşturmuştum.

Kod Örneği: Temel PHP sunucusunu çalıştırma

php

<?php
echo "Hello, World! This is a test of the Apache server.";
?>
Bu kodu index.php dosyasına koyarak, Apache sunucusunu çalıştırdığınızda tarayıcıda "Hello, World!" mesajını görüntüleyebilirsiniz. Bu, yerel web sunucusunun düzgün çalışıp çalışmadığını test etmek için kullanıldı.





Day 2: Setting Up MAMP and Database Configurations

İkinci gün MAMP kurulumu ve MySQL veritabanı yapılandırması üzerine çalıştım. Bu, farklı ortamları test etme esnekliği sağladı ve veritabanı yönetimi konusunda deneyim kazandım.

Kod Örneği: MySQL veritabanı bağlantısı (PHP kullanarak)

php

$servername = "localhost";
$username = "root";
$password = "";
$dbname = "testdb";

// Bağlantı oluştur
$conn = new mysqli($servername, $username, $password, $dbname);

// Bağlantıyı kontrol et
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
?>
Bu kod, PHP kullanarak bir MySQL veritabanına bağlantı kurmanın basit bir yoludur ve veritabanı yapılandırmasını doğrulamak için kullanılmıştır.





Day 3: Initial Project Setup and Troubleshooting

Üçüncü gün proje yapısını oluşturma ve versiyon kontrol sistemi kullanma üzerineydi. Git'i temel olarak yapılandırıp şube oluşturma işlemlerini yaptım.

Kod Örneği: Git şube oluşturma ve ilk push işlemi

bash

# Yeni bir şube oluştur
git checkout -b feature-setup

# Değişiklikleri commit et
git add .
git commit -m "Initial project setup with basic structure"

# Uzak repo'ya push et
git push origin feature-setup
Bu işlemler Git üzerinden proje yönetiminin nasıl yapıldığını gösterdi ve şube kullanımı konusunda pratik yapmamı sağladı.





Day 4: Starting Front-End Development with React.js

Dördüncü gün, React.js ile ön uç geliştirmeye başlandı. Proje yapısı oluşturuldu ve temel bir bileşen yaratıldı.

Kod Örneği: Basit bir React bileşeni

javascript 

import React from 'react';

function Greeting() {
    return (
        <div>
            <h1>Hello, welcome to the project!</h1>
        </div>
    );
}

export default Greeting;
Bu kod, React kullanarak basit bir "Greeting" bileşeni oluşturur ve tarayıcıda bir mesaj görüntüler. Bu örnek, React bileşenlerinin nasıl oluşturulacağını anlamak için temel teşkil eder.





Day 5: Developing Reusable Components in React

Beşinci gün, React'te yeniden kullanılabilir bileşenler oluşturma üzerine odaklanıldı. Formlar, butonlar ve giriş alanları gibi bileşenler geliştirildi.

Kod Örneği: Yeniden kullanılabilir bir buton bileşeni

javascript

import React from 'react';

function Button({ label, onClick }) {
    return (
        <button onClick={onClick} className="btn btn-primary">
            {label}
        </button>
    );
}

export default Button;
Bu kod, farklı işlevlerde kullanılabilecek yeniden kullanılabilir bir buton bileşeni tanımlar. Buton etiketi ve tıklama işlevi props aracılığıyla dinamik olarak ayarlanabilir.





Day 6: Starting Back-End Development with Laravel

Altıncı gün, Laravel ile arka uç geliştirmeye başlandı ve temel yapı kuruldu.

Kod Örneği: Basit bir Laravel rota tanımı

php 

// routes/web.php
use Illuminate\Support\Facades\Route;

Route::get('/welcome', function () {
    return view('welcome');
});
Bu örnek, Laravel'de basit bir rota tanımlar ve /welcome adresine yapılan isteklerde welcome adındaki görünüme yönlendirilir. Bu, rotaların nasıl çalıştığını anlamak için başlangıç niteliğindedir.





Day 7: Expanding the API with CRUD Operations

Yedinci gün, API'nin genişletilmesi ve kullanıcı profilleri için CRUD işlemlerinin eklenmesi üzerineydi.

Kod Örneği: Kullanıcı oluşturma için Laravel'de basit bir API kontrolcüsü

php
 
// app/Http/Controllers/UserController.php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\User;

class UserController extends Controller
{
    public function create(Request $request)
    {
        $user = new User();
        $user->name = $request->input('name');
        $user->email = $request->input('email');
        $user->password = bcrypt($request->input('password'));
        $user->save();

        return response()->json(['message' => 'User created successfully']);
    }
}
Bu kod, yeni bir kullanıcı oluşturmak için bir API kontrolcüsüdür ve gelen isteği işleyerek veritabanına kaydeder.





Day 8: Implementing Middleware and Security Features

Sekizinci gün, Laravel'de güvenlik özellikleri ve middleware uygulamaları geliştirildi.

Kod Örneği: Laravel'de basit bir middleware kullanımı

php
 
// app/Http/Middleware/CheckAdmin.php
namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;

class CheckAdmin
{
    public function handle(Request $request, Closure $next)
    {
        if (!$request->user() || !$request->user()->isAdmin()) {
            return redirect('home');
        }

        return $next($request);
    }
}
Bu middleware, kullanıcının admin olup olmadığını kontrol eder ve admin değilse home sayfasına yönlendirir.





Day 9: Working on the CRM Component in the Front-End

Dokuzuncu gün, CRM bileşenleri üzerinde çalışıldı. Yeni kontak eklemek için form oluşturuldu.

Kod Örneği: React kullanarak basit bir form bileşeni

javascript
 
import React, { useState } from 'react';

function ContactForm() {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');

    const handleSubmit = (e) => {
        e.preventDefault();
        console.log('New Contact:', { name, email });
    };

    return (
        <form onSubmit={handleSubmit}>
            <input
                type="text"
                placeholder="Name"
                value={name}
                onChange={(e) => setName(e.target.value)}
            />
            <input
                type="email"
                placeholder="Email"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
            />
            <button type="submit">Add Contact</button>
        </form>
    );
}

export default ContactForm;
Bu form, kullanıcıdan isim ve e-posta adresi bilgilerini alır ve form gönderildiğinde bilgileri konsola yazdırır.





Day 10: QR Code-Based Gift-Sending Functionality Development

Onuncu gün, QR kod tabanlı hediye gönderme özelliği geliştirildi. Bu özellik için bir QR kod kütüphanesi entegre edildi.

Kod Örneği: JavaScript ile QR kod oluşturma

javascript
 
import QRCode from 'qrcode.react';

function QRCodeGenerator({ text }) {
    return (
        <div>
            <QRCode value={text} size={256} />
        </div>
    );
}

export default QRCodeGenerator;
Bu kod, verilen metin ile bir QR kodu oluşturur ve ekranda görüntüler. QR kodu, hediye detaylarını içerebilir ve kullanıcılar tarafından tarandığında hediye bilgilerini görüntüleyebilir.





Day 11: Integrating QR Code Scanning for Reward Redemption

On birinci gün, ödül alma işlemi için QR kod tarama entegrasyonu yapıldı. Bu özellik, kullanıcıların QR kodları tarayarak ödülleri etkinleştirmesine olanak tanır.

Kod Örneği: React kullanarak QR kod tarama

javascript
 
import React, { useState } from 'react';
import QrReader from 'react-qr-reader';

function QRCodeScanner() {
    const [scanResult, setScanResult] = useState('');

    const handleScan = (data) => {
        if (data) {
            setScanResult(data);
            console.log('Scanned QR Code:', data);
        }
    };

    const handleError = (err) => {
        console.error(err);
    };

    return (
        <div>
            <h2>Scan QR Code</h2>
            <QrReader
                delay={300}
                onError={handleError}
                onScan={handleScan}
                style={{ width: '100%' }}
            />
            <p>Scan Result: {scanResult}</p>
        </div>
    );
}

export default QRCodeScanner;
Bu kod, react-qr-reader kütüphanesini kullanarak QR kodu tarama işlemini gerçekleştirir. Tarama sonucu alındığında, veriler ekranda görüntülenir.





Day 12: Implementing Authentication and Authorization

On ikinci gün, projeye kimlik doğrulama ve yetkilendirme eklendi. JWT (JSON Web Token) tabanlı bir kimlik doğrulama sistemi kullanıldı.

Kod Örneği: Laravel'de JWT kullanarak kimlik doğrulama

php
 
// routes/api.php
use App\Http\Controllers\AuthController;

Route::post('login', [AuthController::class, 'login']);
Route::post('register', [AuthController::class, 'register']);
php
 
// app/Http/Controllers/AuthController.php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\User;
use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Facades\Validator;

class AuthController extends Controller
{
    public function register(Request $request)
    {
        $validator = Validator::make($request->all(), [
            'name' => 'required|string|max:255',
            'email' => 'required|string|email|max:255|unique:users',
            'password' => 'required|string|min:6',
        ]);

        if ($validator->fails()) {
            return response()->json($validator->errors(), 400);
        }

        $user = User::create([
            'name' => $request->name,
            'email' => $request->email,
            'password' => Hash::make($request->password),
        ]);

        $token = $user->createToken('auth_token')->plainTextToken;

        return response()->json(['access_token' => $token, 'token_type' => 'Bearer']);
    }

    public function login(Request $request)
    {
        if (!Auth::attempt($request->only('email', 'password'))) {
            return response()->json(['message' => 'Unauthorized'], 401);
        }

        $user = Auth::user();
        $token = $user->createToken('auth_token')->plainTextToken;

        return response()->json(['access_token' => $token, 'token_type' => 'Bearer']);
    }
}
Bu kod, kullanıcının kayıt olmasını ve giriş yapmasını sağlayan bir kimlik doğrulama kontrolcüsüdür ve JSON Web Token kullanarak kullanıcıya bir erişim belirteci sağlar.





Day 13: Enhancing User Interface with Tailwind CSS

On üçüncü gün, Tailwind CSS ile kullanıcı arayüzü geliştirildi ve sayfa düzeni iyileştirildi.

Kod Örneği: Tailwind CSS kullanarak basit bir düğme stili

javascript
 
function StyledButton({ label, onClick }) {
    return (
        <button
            onClick={onClick}
            className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
        >
            {label}
        </button>
    );
}

export default StyledButton;
Bu örnek, Tailwind CSS kullanarak stil verilmiş bir düğme bileşeni oluşturur. Düğme mavi arka plana sahip ve üzerine gelindiğinde daha koyu bir mavi renge dönüşür.





Day 14: Working on Error Handling and Logging

On dördüncü gün, hata yönetimi ve hata kaydı üzerine çalışıldı. Sistem hatalarının düzgün bir şekilde yönetilmesi için çözümler geliştirildi.

Kod Örneği: Express.js'de hata yönetimi

javascript
 
const express = require('express');
const app = express();

// Basit bir hata işleyici
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Something went wrong!');
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
Bu kod, Express.js uygulamasında basit bir hata işleyici oluşturur. Uygulama hata aldığında, hata yığını konsola yazdırılır ve istemciye hata mesajı gönderilir.





Day 15: Implementing Notifications with Socket.IO

On beşinci gün, Socket.IO kullanarak bildirimler eklenmeye başlandı. Bu özellik, kullanıcılara gerçek zamanlı bildirimler göndermeyi sağlar.

Kod Örneği: Socket.IO ile basit bir sunucu

javascript
 
const io = require('socket.io')(3000);

io.on('connection', (socket) => {
    console.log('A user connected');

    socket.on('sendNotification', (data) => {
        io.emit('receiveNotification', data);
    });

    socket.on('disconnect', () => {
        console.log('A user disconnected');
    });
});
Bu kod, basit bir Socket.IO sunucusu oluşturur ve bağlantı yapan kullanıcılara bildirim gönderebilmek için gerekli olayları tanımlar.





Day 16: Testing and Debugging

On altıncı gün, proje kapsamındaki modüller için testler yazılmaya ve hata ayıklama yapılmaya başlandı.

Kod Örneği: Jest kullanarak basit bir test

javascript
 
// sum.js
function sum(a, b) {
    return a + b;
}
module.exports = sum;

// sum.test.js
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
});
Bu örnek, Jest test çerçevesini kullanarak basit bir test tanımlar ve sum fonksiyonunun doğru sonuç verip vermediğini kontrol eder.





Day 17: Deploying the Application Using Docker

On yedinci gün, uygulamanın Docker kullanarak dağıtımı gerçekleştirildi. Bu işlem, uygulamanın farklı ortamlarda tutarlı bir şekilde çalışabilmesini sağlamak için önemlidir.

Kod Örneği: Basit bir Dockerfile ile Node.js uygulamasını Docker konteynerine alma

dockerfile
 
# Base image olarak Node.js
FROM node:18

# Çalışma dizini oluştur
WORKDIR /app

# Bağımlılık dosyalarını kopyala
COPY package*.json ./

# Bağımlılıkları yükle
RUN npm install

# Uygulama dosyalarını kopyala
COPY . .

# Uygulama çalıştırma
CMD ["npm", "start"]

# Sunucu portunu aç
EXPOSE 3000
Bu Dockerfile, bir Node.js uygulamasını çalıştırmak için gerekli adımları içerir. npm install komutu ile bağımlılıklar yüklenir ve uygulama çalıştırılır.





Day 18: Monitoring and Performance Optimization

On sekizinci gün, uygulamanın performansını izlemek ve optimize etmek için çeşitli araçlar ve yöntemler kullanıldı. Bu kapsamda, yük testi ve uygulama izleme yapıldı.

Kod Örneği: Express.js uygulaması için morgan kullanarak basit bir günlükleme

javascript
 
const express = require('express');
const morgan = require('morgan');
const app = express();

// Morgan middleware'i günlükleme için kullan
app.use(morgan('dev'));

app.get('/', (req, res) => {
    res.send('Hello, World!');
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
Bu örnek, morgan middleware'ini kullanarak HTTP isteklerini günlükler ve uygulamanın performansını izlemeye yardımcı olur.





Day 19: Configuring CI/CD Pipelines

On dokuzuncu gün, sürekli entegrasyon ve sürekli dağıtım (CI/CD) süreçleri yapılandırıldı. GitHub Actions kullanarak otomatik test ve dağıtım süreçleri oluşturuldu.

Kod Örneği: Basit bir GitHub Actions iş akışı

yaml
 
name: Node.js CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Kodları çek
      uses: actions/checkout@v2

    - name: Node.js sürümünü kur
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - name: Bağımlılıkları yükle
      run: npm install

    - name: Testleri çalıştır
      run: npm test
Bu iş akışı, main dalına her kod gönderildiğinde veya çekme isteği oluşturulduğunda testleri otomatik olarak çalıştırır.





Day 20: Finalizing the Project and Writing Documentation

Yirminci ve son gün, projenin tamamlanması ve dökümantasyonun yazılması üzerine çalışıldı. Kodun düzenlenmesi, belgelerin hazırlanması ve projenin son haliyle teslim edilmesi sağlandı.

Kod Örneği: README.md dosyası için örnek içerik
 
# CRM System

This project is aimed at optimizing the trade factor in finance field.

## Features

- User registration and authentication
- Reservation management
- QR code scanning for rewards
- Real-time notifications using Socket.IO

## Technologies Used

- Frontend: React, Tailwind CSS
- Backend: Node.js, Express, Laravel
- Database: MongoDB, MySQL
- Real-time communication: Socket.IO

## Setup Instructions

1. Clone the repository: `git clone https://github.com/TheLastKhan/internship-report.git`
2. Install dependencies: `npm install`
3. Run the application: `npm start`
4. Visit `http://localhost:3000` in your browser.
