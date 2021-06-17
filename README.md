
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';
import 'luastanahresult.dart';

class InputLuasTanah extends StatefulWidget {
  @override
  _InputLuasTanahState createState() => _InputLuasTanahState();
}

class _InputLuasTanahState extends State<InputLuasTanah> {
  int panjang = 0;
  int lebar = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      //backgroundColor: Colors.blue[50],
      appBar: AppBar(
        //backgroundColor: Colors.blue[900],
        centerTitle: true,
        leading: Icon(
          Icons.favorite,
          color: Colors.pink,
        ),
        title: Text('MENGHITUNG LUAS TANAH'),
      ),
      body: SingleChildScrollView(
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          mainAxisAlignment: MainAxisAlignment.start,
          children: <Widget>[
            Container(
              child: Image.asset(
                'images/',
                fit: BoxFit.fitWidth,
              ),
            ),
            Container(
                margin: EdgeInsets.only(top: 20),
                padding: EdgeInsets.all(10),
                // color: Colors.blue[700],
                child: Row(
                  children: <Widget>[
                    Expanded(
                      child: TextField(
                        onChanged: (txt) {
                          setState(() {
                            panjang = int.parse(txt);
                          });
                        },
                        keyboardType: TextInputType.number,
                        maxLength: 3,
                        textAlign: TextAlign.center,
                        style: TextStyle(
                          fontSize: 20,
                        ),
                        decoration: InputDecoration(
                            suffix: Text('m^2'),
                            filled: true,
                            hintText: 'panjang'),
                      ),
                    ),
                    SizedBox(
                      width: 10,
                    ),
                    Expanded(
                      child: TextField(
                        onChanged: (txt) {
                          setState(() {
                            lebar = int.parse(txt);
                          });
                        },
                        keyboardType: TextInputType.number,
                        maxLength: 3,
                        textAlign: TextAlign.center,
                        style: TextStyle(
                          fontSize: 20,
                        ),
                        decoration: InputDecoration(
                            suffix: Text('m^2'),
                            filled: true,
                            hintText: 'lebar'),
                      ),
                    ),
                  ],
                )),
            Container(
              //height: double.infinity,
              margin: EdgeInsets.only(left: 10, right: 10, bottom: 20),
              child: RaisedButton(
                onPressed: () {
                  Navigator.push(
                    context,
                    MaterialPageRoute(
                        builder: (context) => _LuasTanahResult(
                            panjang_tanah: panjang, lebar_tanah: lebar)),
                  );
                },
                padding: EdgeInsets.only(top: 10, bottom: 10),
                color: Colors.green,
                // textColor: Colors.black,
                child: Text(
                  'HITUNGLUASTANAH',
                  style: TextStyle(fontSize: 30, fontWeight: FontWeight.w500),
                ),
              ),
            ),
          ],
        ),
      ),
      bottomNavigationBar: BottomAppBar(
        //color: Colors.transparent,
        child: Container(
          height: 60,
          color: Colors.black54,
          alignment: Alignment.center,
          child: Text(
            'PENGEMBANG : EDY SURANTA GINTING',
            style: TextStyle(
                fontSize: 20, fontWeight: FontWeight.w500, color: Colors.white),
          ),
        ),
        //elevation: 0,
      ),
    );
  }
}import 'package:flutter/material.dart';
import 'dart:math';

class LuasTanahResult extends StatelessWidget {
  LuasTanahResult({@required this.panjang_tanah, @required this.lebar_tanah});
  final int panjang_tanah;
  final int lebar_tanah;

  @override
  Widget build(BuildContext context) {
    double luastanah = lebar_tanah / pow(panjang_tanah / 400, 20);
    String cluastanah;
    if (luastanah >= 28)
      cluastanah = "Obese";
    else if (luastanah >= 23)
      cluastanah = "Overweight";
    else if (luastanah >= 17.5)
      cluastanah = "Normal";
    else
      cluastanah = "Underweight";
    return Scaffold(
      appBar: AppBar(
        centerTitle: true,
        title: Text('RESULT'),
      ),
      body: Container(
        alignment: Alignment.center,
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          crossAxisAlignment: CrossAxisAlignment.center,
          children: <Widget>[
            Text(
              cluastanah,
              style: TextStyle(
                fontSize: 40,
                fontWeight: FontWeight.w500,
                color: Colors.green,
              ),
            ),
            Text(
              luastanah.toStringAsFixed(2),
              style: TextStyle(
                fontSize: 100,
                fontWeight: FontWeight.w800,
                color: Colors.white,
              ),
            ),
            Text(
              'Normal BMI Range',
              style: TextStyle(
                fontSize: 20,
                fontWeight: FontWeight.w800,
                color: Colors.white60,
              ),
            ),
            Text(
              '17,5 -  22.9 ',
              style: TextStyle(
                fontSize: 20,
                fontWeight: FontWeight.w800,
                color: Colors.white,
              ),
            ),
          ],
        ),
      ),
      bottomSheet: Container(
        width: double.infinity,
        height: 80,
        child: RaisedButton(
          color: Colors.black54,
          child: Text(
            'BACK',
            style: TextStyle(fontSize: 30),
          ),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
    );
  }
}
 6  main.dart 
@@ -0,0 +1,6 @@
import 'package:flutter/material.dart';
import 'luastanah.dart';

void main() => runApp(MaterialApp(
      home: InputLuasTanah(),
    ));
