<div class="box-body space-y-4">
            <div class="p-4 bg-gray-100 rounded">
                <h6 class="font-semibold text-lg">1. Autentikasi</h6>
                <p>Gunakan API Key yang telah Anda generate sebagai Bearer Token dalam setiap request.</p>
                <pre class="bg-gray-900 text-white p-3 rounded"><code>Authorization: Bearer YOUR_API_KEY</code></pre>

                <p class="mt-3">Dan kami hanya menerima request dalam bentuk JSON, pastikan di header kamu terdapat.</p>
                <pre class="bg-gray-900 text-white p-3 rounded"><code>Accept: application/json</code></pre>
            </div>

            <div class="p-4 bg-gray-100 rounded">
                <h6 class="font-semibold text-lg">2. Mendapatkan Daftar Bank</h6>

                <p class="mt-3 mb-3"><strong>Endpoint:</strong> Ambil Data Bank (Biaya Rp. 0)</p>
                <pre class="bg-gray-900 text-white p-3 rounded"><code>GET https://storepanda.web.id/api/banklist</code></pre>

                <p class="mt-3 mb-3">Gunakan perintah berikut di **PHP** dengan **cURL**:</p>
                <pre class="bg-gray-900 text-white p-3 rounded"><code>
&lt;?php
$token = "YOUR_API_KEY"; // Ganti dengan API Key Anda
$url = "https://storepanda.web.id/api/banklist"; // Ganti dengan URL API

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    "Authorization: Bearer " . $token,
    "Accept: application/json"
]);

$response = curl_exec($ch);
curl_close($ch);

echo $response;
?&gt;
                </code></pre>
            </div>

            <div class="p-4 bg-gray-100 rounded">
                <h6 class="font-semibold text-lg">3. Penggunaan Cek Rekening</h6>
                <p class="mt-3 mb-3"><strong>Endpoint:</strong> Cek Rekening (Hit Sukses Rp. 100/hit, Hit Gagal Rp. 50/hit)
                </p>
                <p class="">*Rekening tidak ditemukan termasuk dalam Hit Gagal </p>
                <p class="mb-3">*Semua HTTP Code selain 200, termasuk dalam Hit Gagal</p>
                <pre class="bg-gray-900 text-white p-3 rounded"><code>POST https://storepanda.web.id/api/inquiry</code></pre>
                <p class="mt-3">Bank Code = String (Wajib)</p>
                <p>Account Number = String (Wajib)</p>

                <p class="mt-3 mb-3">Gunakan perintah berikut di **PHP** dengan **cURL**:</p>
                <pre class="bg-gray-900 text-white p-3 rounded"><code>
&lt;?php
$token = "YOUR_API_KEY";
$url = "https://storepanda.web.id/api/inquiry";

$data = [
    'bankCode'      =&gt; "your_bank_code",
    'accountNumber' =&gt; "your_account_number",
];

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    "Authorization: Bearer " . $token,
    "Content-Type: application/json"
]);

$response = curl_exec($ch);
curl_close($ch);

echo $response;
?&gt;
                </code></pre>
            </div>

            <div class="p-4 bg-gray-100 rounded">
                <h6 class="font-semibold text-lg">4. Contoh Response</h6>
                <pre class="bg-gray-900 text-white p-3 rounded"><code>{
    "status": 200,
    "message": "Rekening ditemukan.",
    "data": {
        "bank": "Bank Central Asia",
        "rekening": "013xxxx",
        "name": "MUxxxxxx",
        "saldo": "6600"
    }
}</code></pre>
            </div>
        </div>
