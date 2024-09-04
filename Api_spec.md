API Spec: Fitur Peminjaman Uang

# FITUR LOANS

Base URL:
`https://api.example.com/v1/loans`

## Authentication
## Semua endpoint harus menggunakan autentikasi berbasis token (JWT). Token harus disertakan di setiap request melalui header:
```
Authorization: Bearer <token>
```
# Endpoints:
## 1. POST /loans/request
### Deskripsi: Mengajukan permohonan peminjaman uang.

Request Body:

```JSON
{
  "borrowerId": "string",       // ID peminjam
  "amount": "number",           // Jumlah uang yang dipinjam
  "durationInMonths": "number", // Durasi peminjaman dalam bulan
  "purpose": "string"           // Tujuan peminjaman
}

```
Response:

- 201 Created
```JSON
{
  "loanId": "string",
  "borrowerId": "string",
  "amount": "number",
  "durationInMonths": "number",
  "interestRate": "number",  // Suku bunga
  "status": "Pending",       // Status awal permohonan
  "createdAt": "string",     // Tanggal permohonan dibuat
  "updatedAt": "string"
}
```

- 400 Bad Request
```JSON
{
  "error": "Invalid input data"
}
```
## 2. GET /loans/(loanId)
### Deskripsi: Mendapatkan detail permohonan peminjaman berdasarkan ID peminjaman.

Path Parameter:
`loanId`: ID dari permohonan pinjaman yang akan ditampilkan.

Response:

- 200 OK

```JSON
{
  "loanId": "string",
  "borrowerId": "string",
  "amount": "number",
  "durationInMonths": "number",
  "interestRate": "number",
  "status": "Pending | Approved | Rejected",  // Status pinjaman
  "createdAt": "string",
  "updatedAt": "string"
}

```
- 404 Not Found
```JSON
{
  "error": "Loan not found"
}
```

## 3. PUT /loans/{loanId}/approve
### Deskripsi: Menyetujui permohonan pinjaman.

Path Parameter:
`loanId`: ID dari permohonan pinjaman yang akan di setujui

Response:

- 200 OK
```JSON
{
  "loanId": "string",
  "status": "Approved",
  "approvedAt": "string"  // Tanggal persetujuan
}
```
- 404 Not Found
```JSON
{
  "error": "Loan not found"
}
```

## 4. PUT /loans/{loanId}/reject
### Deskripsi: Menolak permohonan pinjaman.

Path Parameter:
`loanId`: ID dari permohonan pinjaman yang akan ditolak.

Response:

- 200 OK
```JSON
{
  "loanId": "string",
  "status": "Rejected",
  "rejectedAt": "string"  // Tanggal penolakan
}
```
- 400 OK 
```JSON
{
  "error": "Loan not found"
}
```
## 5. GET /loans/borrower/{borrowerId}
### Deskripsi: Mendapatkan daftar pinjaman yang diajukan oleh peminjam tertentu.

Path Parameter:
`borrowerId`: ID peminjam.

Response:
- 200 OK
```JSON
[
  {
    "loanId": "string",
    "amount": "number",
    "durationInMonths": "number",
    "interestRate": "number",
    "status": "Pending | Approved | Rejected",
    "createdAt": "string",
    "updatedAt": "string"
  }
]
```

- 404 Not Found
```JSON
{
  "error": "Borrower not found"
}
```
## 6. DELETE /loans/{loanId}
### Deskripsi: Menghapus permohonan pinjaman yang belum disetujui atau ditolak.

Path Parameter:
`loanId`: ID dari permohonan pinjaman yang akan dihapus.

Response:

- 200 OK
```JSON 
{
  "message": "Loan deleted successfully"
}
```
- 404 Not Found
```JSON
{
  "error": "Loan not found"
}
```











