---
title: Konfigurasi Awal JavaFX di Intellij Idea
date: 2022-11-10 11:12:00 +0700
categories: [Blogging, Tutorial]
tags: [java, javafx, intellij, java 17, amazon coretto]
---

## Pengenalan JavaFX
JavaFX merupakan salah satu framework untuk membangun aplikasi desktop. JavaFX ditulis menggunakan bahasa Java
sehingga di JavaFX dapat digunakan fitur-fitur yang ada di Java seperti multithreading, generics, dan lambda expression.
Selain membangun aplikasi menggunakan bahasa Java, dapat juga menggunakan bahasa yang didukung JVM lainnya, seperti
Kotlin, Groovy dan Scala.

Pada JavaFX GUI dikonstruksikan sebagai *scene graph*. Sebuah *scene graph* merupakan kumpulan-kumpulan dari elemen visual,
yang disebut sebagai *nodes* yang diatur secara hierarkis. Sebuah *scene graph* dibangun menggunakan API publik JavaFX.
*Nodes* di sebuah *scene graph* dapat mengurus input dan gesture dari user, selain itu juga *nodes* dapat memiliki
efek, transformasi, dan *states*. Beberapa tipe dari *nodes* yang ada di *scene graph* dapat berupa *UI Controls* seperti
*buttons*, *text fields*, bentuk dari benda 2D dan 3D, *images*, media seperti audio dan video, konten web, dan *charts*.

## Konfigurasi JavaFX

### Mengunduh dan Mengekstrak SDK JavaFX
Untuk mengunduh SDK JavaFX dapat pergi ke link berikut [https://gluonhq.com/products/javafx](https://gluonhq.com/products/javafx/)
silahkan pilih JavaFX versi 17. Setelah diunduh silahkan di ekstrak, lokasi ekstrak dapat di lokasi mana saja

![contoh lokasi ekstrak](/posts/20221110/01-ekstrak-sdk-javafx.png)

### Buat Project Baru di Intellij
Kemudian buat project baru di Intellij pastikan menggunakan JDK versi 17
![buat_project_baru](/posts/20221110/02-buat-project-baru.png)

### Menambahkan Library dan Module JavaFX
Untuk menambahkan library dan module silahkan klik <kbd>File > Project Structure</kbd> pada menubar. Setelah itu pada
<kbd>Project Settings</kbd> pilih <kbd>Libraries</kbd>, dan silahkan tambahkan library dari JavaFX yang telah diekstrak sebelumnya,
pastikan pilih subfolder ***lib*** saja yang dipilih kemudian klik <kbd>Apply</kbd>
![menambahkan_library](/posts/20221110/03-menambahkan-library-javafx.png)

Setelah menambahkan library barulah menambahkan module, caranya adalah di <kbd>Project Settings</kbd> pilih <kbd>Modules</kbd>
dan pada bagian <kbd>Export</kbd> silahkan tambahkan library yang telah kamu tambahkan tadi pada kasus penulis disini bernama
lib kemudian klik <kbd>Apply</kbd> lalu <kbd>Ok</kbd>

![menambahkan_modules](/posts/20221110/04-menambahkan-module.png)

### Menulis Kode
Pada tahap sebelumnya sudah dilakukan menambahkan library dan module JavaFX pada proyek, kemudian pada tahap ini akan menulis kode
sederhana. Kode ini akan menampilkan tulisan Hello World ke layar, kode ini mempunyai satu buah root node dan node text.

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.layout.VBox;
import javafx.scene.text.Text;
import javafx.stage.Stage;

public class HelloFXApp extends Application
{
    public static void main(String[] args)
    {
        Application.launch(args);
    }


    // this method will be called for the first time
    @Override
    public void start(Stage stage) throws Exception
    {
        // Create a root VBox node
        VBox root = new VBox();

        // create a text node
        Text msg = new Text("Hello World");

        // add the text node to the vbox as a child node
        root.getChildren().add(msg);

        // create a scene
        Scene scene = new Scene(root, 300, 50);

        // Set the scene to the stage
        stage.setScene(scene);

        // Set a title for the stage
        stage.setTitle("JavaFX Application");

        // Show the stage
        stage.show();
    }
}

```

### Menambahkan VM Options
Setelah menulis kode sebelum menjalankan, silahkan klik dahulu <kbd>Run > Configurations...</kbd> setelah itu tambahkan
field VM Options yang berisi `--module-path="LOKASI_TEMPAT_EKSTRAK\JavaFx\openjfx-19_windows-x64_bin-sdk\javafx-sdk-19\lib" --add-modules=javafx.controls`
jika field VM Options tidak muncul coba klik ***Modify Options*** lalu pilih <kbd>Add VM Options</kbd> kemudian klik <kbd>Ok</kbd>

![menambahkan_vm_options](/posts/20221110/05-menambahkan-vm-arguments.png)

### Hasil
Kemudian silahkan jalankan code tersebut dengan biasa yaitu mengklik tombol run hijau disamping public class maka akan muncul
panel baru yang menampilkan tulisan Hello World

![hello_world](/posts/20221110/06-hasil-run.png)
