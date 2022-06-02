FROM kasmweb/core-ubuntu-focal:develop
USER root

ENV HOME /home/kasm-default-profile
ENV STARTUPDIR /dockerstartup
ENV INST_SCRIPTS $STARTUPDIR/install
WORKDIR $HOME


######### Customize Container Here ###########

RUN apt update && apt -y upgrade && apt -y install mc unzip firefox

# Install XFCE Dark Theme
RUN apt install numix-gtk-theme

# Install Hack Nerd Font
RUN wget -q https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Hack.zip && unzip Hack.zip -d /usr/local/share/fonts

# Install Starship
RUN wget -q https://starship.rs/install.sh && chmod +x install.sh && ./install.sh -y

# Add Starship to bashrc
RUN echo 'eval "$(starship init bash)"' >> .bashrc

# Add Starship Theme
COPY config/starship.toml .config/starship.toml

# Change Background to sth cool
COPY assets/wallpaper.jpg  /usr/share/extra/backgrounds/bg_default.png

# Disable sslOnly 
COPY config/vnc_startup.sh /dockerstartup/vnc_startup.sh

######### End Customizations ###########

RUN chown 1000:0 $HOME
RUN $STARTUPDIR/set_user_permission.sh $HOME

ENV HOME /home/kasm-user
WORKDIR $HOME
RUN mkdir -p $HOME && chown -R 1000:0 $HOME
USER kasm-user
