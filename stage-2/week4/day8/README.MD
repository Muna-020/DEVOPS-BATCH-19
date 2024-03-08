# Terraform
```
Terraform adalah sebuah tool open-source yang digunakan untuk melakukan provisioning, manajemen, dan deployment infrastruktur secara otomatis dan terdokumentasi. 
Dikembangkan oleh HashiCorp, Terraform memungkinkan pengguna untuk mendefinisikan infrastruktur mereka sebagai kode (Infrastructure as Code/IaC) menggunakan format konfigurasi yang deklaratif.

Tahap ringkas dalam pengunaan Terraform:
1. melakukan persiapan akun pada AWS Cloud dengan metode free claim
2. menginstall Terraform pada server lokal 
3. membuat sebuah direktori dan file denagan ekstensi `.tf` untuk persiapan terraform lalu menginisiasi dengan command `terraform init`
4. kemudian membuat konfigurasi pada file `.tf` untuk meneentukan sumber daya infrastruktur yang ingin Anda kelola, seperti instance server, database, jaringan, dan lainnya.
5. setelah konfigurasi siap lalu melakukan perencanaan dengan `terraform plan` untuk mengetahui konfigurasi sudah siap lalu melakukan running terraform dengan `terraform apply`
6. setelah melakukan apply dapat dilihat pada AWS Cloud Instance bahwa server telah berhasil dibuat

```
+ Berikut gambaran dan script konfigurasi dari hasil pengerjaan ringkas terraform:


```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
    region = "ap-southeast-2"
    access_key = "AKIA6GBMECVM2RFIXN7W"
    secret_key = "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"
}

resource "tls_private_key" "rsa_4096" {
    algorithm = "RSA"
    rsa_bits = "4096"
}

variable "key_name" {}

resource "aws_key_pair" "key_pair" {
    key_name = var.key_name
    public_key = tls_private_key.rsa_4096.public_key_openssh
}

resource "local_file" "private_key" {
    content = tls_private_key.rsa_4096.private_key_pem
    filename = var.key_name
}

resource "aws_instance" "terraform_aws_ubuntu" {
    ami = "ami-0d6f74b9139d26bf1"
    instance_type = "t2.micro"
    key_name = aws_key_pair.key_pair.key_name

    tags = {
        Name = "terraform_aws_ubuntu"
    }
}
```

![Screenshot from 2024-03-08 10-27-24](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ccb4590b-0bf7-409e-b00e-4369dd4e95eb)

![Screenshot from 2024-03-08 10-15-36](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/1ecfc3f0-15ee-44f4-b0d2-d519bf997dab)

![Screenshot from 2024-03-08 10-16-42](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/c05aa2dd-04c8-4156-af45-7408a9ab0b3a)

![Screenshot from 2024-03-08 10-24-19](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/3a4f071b-d35a-47ae-9bfd-f748c87d1448)

