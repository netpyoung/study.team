# Redmine
* http://www.redmine.org/
* Redmine�� ������ ������Ʈ ���� �� ���ø����̼��̴�. Ruby on Rails �����ӿ�ũ�� �̿��ؼ� �ۼ��Ǿ���, ũ�ν� �÷����� ũ�ν� �����ͺ��̽��� �����Ѵ�.
* Redmine�� ���¼ҽ��̸�, GNU General Public License v2 (GPL)�Ͽ� �����ǰ� �ִ�.
* ��ġ
 - http://www.redmine.org/projects/redmine/wiki/RedmineInstall
 - http://www.redmine.or.kr/projects/community/wiki/���帶��_��ġ(Windows) ����.

# MySQL
* http://dev.mysql.com/downloads/

```cmd
> mysqld --install 

// �������� ���� ������,
> mysql -uroot
```
# PostgreSQL
* http://www.postgresql.org/
* PostgreSQL�� ������ ���¼ҽ� ��ü-���� �����ͺ��̽� �ý����̴�.


# Bundler
* http://gembundler.com/
* Bundler�� ruby ���ø����̼� ȯ���� �ϰ��ǰ� ����������.
* ������ �ʿ��� ��Ȯ�� gem(�׸��� ����)�� �׻� ����.

# DevKit
* https://github.com/oneclick/rubyinstaller/wiki/Development-Kit
* DevKit�� ��������� Ruby�� ���� ����Ƽ�� C/C++ Ȯ���� ����/����� ���� ����� �ִ� ����.

config.yml

```yml
---
- C:\Ruby200-x64
```

```cmd
c:\DevKit> ruby dk.rb init

// config.yml������,
c:\DevKit> ruby dk.rb install
```

--------------------------------------------------------------------------------

# Trouble Shooting

## The 'json' native gem requires installed build tools.
* http://rubyinstaller.org/downloads ����, DEVELOPMENT KIT ��ġ


--------------------------------------------------------------------------------

# In Archlinux
* ���� : https://wiki.archlinux.org/index.php/Redmine

* ruby ��ġ.

```cmd
$ yaourt -S ruby
$ sudo gem install bundler
```
~/.gem/ruby/x.x.x/bin�� PATH�� �߰�������.

* db ��ġ

```cmd
$ yaourt -S mariadb
$ sudo systemctl start mysqld
$ mysql -u root
```

```sql
CREATE DATABASE redmine CHARACTER SET UTF8;
CREATE USER 'redmine'@'localhost' IDENTIFIED BY '1234';
GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost';
```

* redmine ��ġ

```cmd
$ yaourt -S mercurial
$ hg clone --updaterev 2.3-stable https://bitbucket.org/redmine/redmine-all redmine
$ cd redmine
redmine$ cp config/database.yml.example config/database.yml
redmine$ vi config/database.yml
```

```yml
production:
  adapter: mysql2
  database: redmine
  host: localhost
  username: redmine
  password: "1234"
  encoding: utf8
```

```cmd
redmine$ sudo bundle install --without development test rmagick
redmine$ rake generate_secret_token
redmine$ RAILS_ENV=production rake db:migrate

redmine$ RAILS_ENV=production REDMINE_LANG=ko rake redmine:load_default_data
redmine$ sudo chmod -R 755 files/ log/ tmp/ public/
redmine$ sudo ruby script/rails server webrick -e production
```

���� : http://localhost:3000/
���̵�/��� : admin / admin


webrick�� �׽�Ʈ�뵵�θ� ����.

Passenger �÷����ΰ�, Nginx�� ��ġ �� ����������.


# plugin
```cmd
redmine$ cd plugins
redmine/plugins$ sudo gem install redcarpet
redmine/plugins$ git clone https://github.com/alminium/redmine_redcarpet_formatter.git
redmine/plugins$ cd redmine_redcarpet_formmatter
redmine/plugins/redmine_redcarpet_formmatter$ git checkout v2.0.1
```

Admin -> Settings -> Text formatting���� �ٲ��ֱ⸸ �ϸ� ��-_-.


# theme
* http://redminecrm.com/pages/a1-theme
 - ����� ȸ�� ����.�����ѵ�?
* http://pixel-cookers.github.io/redmine-theme/
 - ���迭, ���̾ƿ��� �ٲ?
* https://github.com/lqez/redmine-theme-basecamp-with-icon
 - ��Ʈķ���̿��Ѱ� ����ϳ�.

```cmd
redmine/public/themes$ git clone git://github.com/lqez/redmine-theme-basecamp-with-icon.git
```