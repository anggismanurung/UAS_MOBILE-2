# UAS_MOBILE-2

import 'package:flutter/material.dart';

  
void main() => runApp(App13());

class App13 extends StatelessWidget {
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Anggi S Manurung',
      home: Anggi6SIA1(),
    );
  }
}

class Anggi6SIA1 extends StatefulWidget {
  MyTabsState createState() => new MyTabsState();
}

class MyTabsState extends State<Anggi6SIA1>
    with SingleTickerProviderStateMixin {
  TabController controller;
  var _scaffoldKey = new GlobalKey<ScaffoldState>();

  void initState() {
    super.initState();
    controller = new TabController(vsync: this, length: 2);
  }

  void dispose() {
    controller.dispose();
    super.dispose();
  }

  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldKey,
      appBar: AppBar(
        leading: IconButton(
            icon: Icon(Icons.menu),
            onPressed: () => _scaffoldKey.currentState.openDrawer()),
        title: Text('Anggi S Manurung'),
        actions: <Widget>[
          IconButton(icon: Icon(Icons.search), onPressed: () {}),
          IconButton(icon: Icon(Icons.more_vert), onPressed: () {}),
        ],
        bottom: TabBar(controller: controller, tabs: <Tab>[
          Tab(text: "Input Data"),
          Tab(text: "Kalkulator"),
        ]),
      ),
      // body: TabBarView(),
      body: TabBarView(controller: controller, children: <Widget>[
        Mahasiswa(),
        Kalkulator(),
      ]),
      drawer: Menu(),
    );
  }
}
class DataMahasiswa{
  String nama;
  String jurusan;
  String jkelamin;
  
  
  DataMahasiswa({this.nama, this.jurusan, this.jkelamin});
  
}

// class Mahasiswa
class Mahasiswa extends StatefulWidget {
  _MyappState createState() => _MyappState();
}

class _MyappState extends State<Mahasiswa> {
  //deklarasi variabel
  final txtnamamhs = TextEditingController();
  final txtjurusan = TextEditingController();
  final txtjkelamin = TextEditingController();
  

  List<Widget> data = [];

  onTambah() {
    setState(() {
      data.add(ListTile(
        leading: Icon(Icons.people),
        title: Text(txtnamamhs.text),
        subtitle: Text(txtjkelamin.text),
        trailing: Text(txtjurusan.text),
      ));
      txtnamamhs.clear();
      txtjurusan.clear();
      txtjkelamin.clear();
    });
  }

  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        new Container(
          padding: EdgeInsets.all(10.0),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: <Widget>[
              TextField(
                controller: txtnamamhs,
                decoration: InputDecoration(hintText: 'Nama Mahasiswa'),
              ),
              TextField(
                controller: txtjurusan,
                decoration: InputDecoration(hintText: 'Jurusan'),
              ),
              TextField(
                controller: txtjkelamin,
                decoration: InputDecoration(hintText: 'Jenis Kelamin'),
              ),
              Divider(height: 5.0),
              ElevatedButton(child: Text("Tambah"), onPressed: onTambah),
            ],
          ),
        ),
        new Column(
          children: data,
        )
      ],
    );
  }
}

// class Menu
class Menu extends StatelessWidget {
  Widget build(BuildContext context) {
    return Drawer(
        elevation: 50.0,
        child: ListView(
          padding: EdgeInsets.zero,
          children: <Widget>[
            UserAccountsDrawerHeader(
              accountName: Text('Anggi S Manurung'),
              accountEmail: Text('anggismanurung2000@gmail.com'),
              currentAccountPicture: Image.network(
                      'https://lh3.googleusercontent.com/ogw/ADea4I6BGqsB4lCA2f_pG800BeBSlnmCMU3T1-H7NAu7=s32-c-mo'),
              decoration: BoxDecoration(color: Colors.blueAccent),
            ),
            ListTile(
              leading: Icon(Icons.account_circle),
              title: Text('UAS Mobile 2'),
              onTap: () {},
            ),
            Divider(height: 2.0),
            ListTile(
              leading: Icon(Icons.accessibility),
              title: Text('Sistem Informasi'),
              onTap: () {},
            ),
            Divider(height: 2.0),
            ListTile(
              leading: Icon(Icons.account_balance),
              title: Text('STMIK Triguna Dharma'),
              onTap: () {},
            ),
            Divider(height: 2.0),
            ListTile(
              leading: Icon(Icons.exit_to_app),
              title: Text('Keluar'),
              onTap: () {
                Navigator.pop(context);
              },
            )
          ],
        ));
  }
}

class Kalkulator extends StatefulWidget {
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<Kalkulator> {
  final txtharga = TextEditingController();
  final txtbeli = TextEditingController();

  String hasil = '' ;
  String bonus = '';
  
  onHitung() {
    setState(() {
      var harga = int.parse(txtharga.text);
      var beli = int.parse(txtbeli.text);
      var bayar = harga * beli;
      hasil = bayar.toString();
      if (bayar > 39999) {
        bonus = "Selamat anda mendapat bonus ";
  } 
    });
  }
  
  
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(20.0),
      child: Column(
        children: <Widget>[
          TextField(
            controller: txtharga,
            decoration: new InputDecoration(
              labelText: "Input Harga",
            ),
          ),
          TextField(
            controller: txtbeli,
            decoration: new InputDecoration(
              labelText: "Input Jumlah Beli",
            ),
          ),
          ElevatedButton(
            child: Text("Hitung"),
            onPressed: onHitung,
          ),
          Text("Total Belanja = Rp.$hasil"),
          Text("$bonus"),
          Text(""),
          Text("Anggi S Manurung"),
        ],
      ),
    );
  }
}
