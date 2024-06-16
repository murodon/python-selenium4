FROM public.ecr.aws/lambda/python:3.12-x86_64

COPY app.py requirements.txt ./
RUN python3.12 -m pip install -r requirements.txt -t .

# selenium-managerを使ってChromeとChromeDriverをダウンロードする。
RUN /var/task/selenium/webdriver/common/linux/selenium-manager --browser chrome --cache-path /opt
# Chromeの依存関係をインストールする。
# 参考: https://qiita.com/hideki/items/d1ff83e7e82afc0c0502
RUN dnf install -y atk cups-libs gtk3 libXcomposite alsa-lib \
        libXcursor libXdamage libXext libXi libXrandr libXScrnSaver \
        libXtst pango at-spi2-atk libXt xorg-x11-server-Xvfb \
        xorg-x11-xauth dbus-glib dbus-glib-devel nss mesa-libgbm \
        libgbm libxkbcommon libdrm

# Command can be overwritten by providing a different command in the template directly.
CMD ["app.lambda_handler"]