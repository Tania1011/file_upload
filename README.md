# Django File Handling — Upload Images from File or URL

A Django project demonstrating file uploads from a local disk or a remote URL using Django generic class-based views (CBVs), ModelForms, and `ImageField`.

This project focuses on practical backend concepts including:

- File uploads
- Media handling
- Image storage
- CRUD operations
- Remote file downloading
- Django forms
- Generic class-based views

---

# Features

- Create, Read, Update, Delete (CRUD) for products
- Upload product images from local files
- Upload product images from remote image URLs
- Automatic image download and storage
- Django generic class-based views
- Image preview support
- Media file serving during development
- Plain semantic HTML templates
- Django ModelForms
- File validation concepts
- Clean project structure

---

# Technologies Used

| Technology | Purpose |
|---|---|
| Python | Backend programming |
| Django | Web framework |
| Pillow | Image handling |
| Requests | Download remote images |
| HTML | Templates |
| SQLite | Default database |

---

# Project Structure

```text
fileproject/
│
├── catalog/
│   ├── migrations/
│   ├── templates/
│   │   └── catalog/
│   │       ├── base.html
│   │       ├── product_list.html
│   │       ├── product_detail.html
│   │       ├── product_form.html
│   │       └── product_confirm_delete.html
│   │
│   ├── admin.py
│   ├── forms.py
│   ├── models.py
│   ├── urls.py
│   └── views.py
│
├── media/
├── fileproject/
├── manage.py
└── requirements.txt
```

---

# Installation

## 1. Clone the Repository

```bash
git clone https://github.com/Tania1011/file_upload.git
cd fileproject
```

---

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv venv
source venv\Scripts\activate
```

### macOS/Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install django pillow requests
```

---

## 4. Apply Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## 5. Run the Development Server

```bash
python manage.py runserver
```

Open in browser:

```text
http://127.0.0.1:8000/
```

---

# Product Model

```python
class Product(models.Model):
    name        = models.CharField(max_length=255)
    description = models.TextField(blank=True)
    price       = models.DecimalField(max_digits=10, decimal_places=2)
    picture_1   = models.ImageField(upload_to='products/', blank=True, null=True)
    picture_2   = models.ImageField(upload_to='products/', blank=True, null=True)
```

---

# File Upload Functionality

This project demonstrates two types of image uploads:

## 1. Local File Upload

Users can upload images directly from their computer using HTML file inputs.

```html
<form method="post" enctype="multipart/form-data">
```

`multipart/form-data` is required for file uploads.

---

## 2. Remote URL Upload

Users can paste a direct image URL.

Example:

```text
https://example.com/image.jpg
```

The application:

1. Sends an HTTP request using `requests`
2. Downloads the image
3. Converts it into a Django `ContentFile`
4. Saves it through `ImageField`

---

# CRUD Operations

The application uses Django generic class-based views:

| View | Purpose |
|---|---|
| `ListView` | Display all products |
| `DetailView` | Display single product |
| `CreateView` | Create products |
| `UpdateView` | Edit products |
| `DeleteView` | Delete products |

---

# Media Handling

## settings.py

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

---

## urls.py

```python
urlpatterns += static(
    settings.MEDIA_URL,
    document_root=settings.MEDIA_ROOT
)
```

---

# How Django Stores Uploaded Files

When a user uploads an image:

```text
Browser
   ↓
request.FILES
   ↓
ModelForm
   ↓
ImageField
   ↓
MEDIA_ROOT/products/
```


# Example Workflow

## Upload from Local Disk

1. Click "Choose File"
2. Select image
3. Submit form
4. Image saved to `media/products/`

---

## Upload from URL

1. Paste image URL
2. Submit form
3. Django downloads image
4. Image stored locally


---


# Screenshots

## All Product List Page

![Product_List Page](screenshots/all_products.png)

---

## Add Product Create Form

![AddProduct Page](screenshots/add_product.png)

---

## Edit Product Edit Form

![EditProduct Page](screenshots/edit_product.png)

