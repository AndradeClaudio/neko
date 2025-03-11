ARG BASE_IMAGE=neko_base
FROM $BASE_IMAGE

ARG SRC_URL="https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb"

#
# install google chrome
RUN set -eux; apt-get update; \
    wget -O /tmp/google-chrome.deb "${SRC_URL}"; \
    apt-get install -y --no-install-recommends openbox /tmp/google-chrome.deb; \
    #
    # clean up
    apt-get clean -y; \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*
# Gere um machine-id estático ou dinâmico
RUN dbus-uuidgen --ensure=/etc/machine-id
# Opcionalmente, vincule /var/lib/dbus/machine-id a /etc/machine-id
RUN ln -sf /etc/machine-id /var/lib/dbus/machine-id
#
# copy configuation files
COPY supervisord.conf /etc/neko/supervisord/google-chrome.conf
COPY --chown=neko preferences.json /home/neko/.config/google-chrome/Default/Preferences
COPY policies.json /etc/opt/chrome/policies/managed/policies.json
COPY openbox.xml /etc/neko/openbox.xml
