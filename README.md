#  Flutter Web Pick Image and Upload to Server | Flutter Web Upload Image to REST API

Here is step by step tutorial about how to upload images or files to Server using flutter web.

[![Watch Tutorial](https://img.youtube.com/vi/jZIixqTkYQI/0.jpg)](https://www.youtube.com/watch?v=jZIixqTkYQI)

## Getting Started

 Dependencies: 
- [http:](https://pub.dev/packages/http)

## Imports
```
import 'dart:typed_data';
import 'dart:html' as html;
import 'package:http_parser/http_parser.dart';
import 'dart:convert';
import 'package:http/http.dart' as http;
import 'package:flutter/material.dart';
```

### Pick Image or File
```
html.FileUploadInputElement uploadInput = html.FileUploadInputElement();
    uploadInput.multiple = true;
    uploadInput.draggable = true;
    uploadInput.click();

    uploadInput.onChange.listen((event) {
      final files = uploadInput.files;
      final file = files![0];
      final reader = html.FileReader();

      reader.onLoadEnd.listen((event) {
        setState(() {
          _bytesData =
              Base64Decoder().convert(reader.result.toString().split(",").last);
          _selectedFile = _bytesData;
        });
      });
      reader.readAsDataUrl(file);
    });
```

### Upload Image or File to Server
```
 var url = Uri.parse("API URL HERE...");
    var request = http.MultipartRequest("POST", url);
    request.files.add(await http.MultipartFile.fromBytes('file', _selectedFile!,
        contentType: MediaType('application', 'json'), filename: "Any_name"));

    request.send().then((response) {
      if (response.statusCode == 200) {
        print("File uploaded successfully");
      } else {
        print('file upload failed');
      }
    });
```


