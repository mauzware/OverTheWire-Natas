# Natas30 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas30
Password: WQhx1BvcmP9irs2MP9tRnLsNaDI76YrH
URL:      http://natas30.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- PERL SQLI TIME BABYYYYYYYYYYYYYYY!

  ```
  #!/usr/bin/perl
  use CGI qw(:standard);
  use DBI;
  
  print <<END;
  Content-Type: text/html; charset=iso-8859-1
  
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas30", "pass": "<censored>" };</script></head>
  <body oncontextmenu="javascript:alert('right clicking has been blocked!');return false;">
  
  <!-- morla/10111 <3  happy birthday OverTheWire! <3  -->
  
  <h1>natas30</h1>
  <div id="content">
  
  <form action="index.pl" method="POST">
  Username: <input name="username"><br>
  Password: <input name="password" type="password"><br>
  <input type="submit" value="login" />
  </form>
  END
  
  if ('POST' eq request_method && param('username') && param('password')){
      my $dbh = DBI->connect( "DBI:mysql:natas30","natas30", "<censored>", {'RaiseError' => 1});
      my $query="Select * FROM users where username =".$dbh->quote(param('username')) . " and password =".$dbh->quote(param('password')); 
  
      my $sth = $dbh->prepare($query);
      $sth->execute();
      my $ver = $sth->fetch();
      if ($ver){
          print "win!<br>";
          print "here is your result:<br>";
          print @$ver;
      }
      else{
          print "fail :(";
      }
      $sth->finish();
      $dbh->disconnect();
  }
  
  print <<END;
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  END
  ```

- Exploitation is explained in the script comments.

  ```
  $ python3 natas30-perlSQLI.py  
  win!<br>here is your result:<br>natas31m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y<div id="viewsource"><a href="index-source.htm
  l">View sourcecode</a></div>
  ```

---

## 🏁 Password for the next level

`Password for natas31 is: m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
