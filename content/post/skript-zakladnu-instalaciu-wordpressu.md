+++
date = "2016-10-14T20:45:36+01:00"
title = "Skript na základnú inštaláciu wordpressu"
categories = ["web-dev"]
tags = ["php","wordpress","bash","web","development"]
comments = false
description = ""
url = "/web-dev/skript-zakladnu-instalaciu-wordpressu/"

+++
V prípade, že mám prístup k serveru SSH alebo inštalujem na localhoste, tento skriptík zrýchli počiatočnú inštaláciu a konfiguráciu wordpressu.

Príkaz wp je [WP-CLI](https://wp-cli.org/)

Postup na [inštaláciu WP-CLI nájdete tu](https://wp-cli.org/docs/installing/).

Pred spustení je treba:

 - vyrobiť databázu,
 - upraviť skript
 - nastaviť prístupy do DB
 - doménu
 - názov webu
 - meno admin účtu
 - heslo
 - email

Potom stačí skript spustiť v priečinku, v ktorom chceme mať WP nainštalovaný.

```sh
#!/usr/bin/sh
# nastavi prava, aby som mohol instalovat
# sudo chmod g+rws .

# stiahne wp
wp core download

#nastavi config.php a pristup do db
wp core config –dbname=DATABASE –dbuser=USER –dbpass=PASSWORD

#nainstaluje wp
wp core install –url=domena.sk –title=NovyWeb –admin_user=menoadmina –admin_password=PASSWORD –admin_email=email@admina.sk

#nastavi slovencinu
wp core language install sk_SK –activate

# aktualizuje, pluginy, temy a jazyky
wp plugin update –all

# nainstaluje a aktivuje najpouzivanejsie pluginy
wp plugin install contact-form-7 wordpress-seo nextgen-gallery easy-fancybox siteorigin-panels child-theme-configurator –activate

# iba nainstaluje pluginy

wp plugin install w3-total-cache woocommerce woocommerce-menu-bar-cart polylang \
google-analytics-dashboard-for-wp multisite-enhancements postman forge disable-emojis \
cpo-widgets cpo-shortcodes advanced-custom-fields adminer
```

