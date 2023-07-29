<ac:layout><ac:layout-section ac:type="single"><ac:layout-cell><h2>Mountebank Installation:<ac:structured-macro ac:name="anchor" ac:schema-version="1" ac:macro-id="479e7d6e-f75c-4c5b-88d9-f84d4cd33180"><ac:parameter ac:name="">mb_local</ac:parameter></ac:structured-macro></h2><h4>Pre-requisites:</h4><ul><li>Javascript (NodeJS)</li><li>NPM<br><br></li></ul><p>Installing mountebank is really simple, just run the following command in your terminal</p><ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="b82fe9bf-d06b-4a69-a346-d8da22de9be2"><ac:parameter ac:name="language">bash</ac:parameter><ac:plain-text-body><![CDATA[npm install -g mountebank]]></ac:plain-text-body></ac:structured-macro><p><br></p><p>In some scenarios you may need to allow for unsafe permissions in npm for it to install properly:</p><ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="67019c31-b911-4460-9443-e93d6dacf9e8"><ac:parameter ac:name="language">bash</ac:parameter><ac:plain-text-body><![CDATA[npm set unsafe-perm true]]></ac:plain-text-body></ac:structured-macro><p class="auto-cursor-target"><br></p><p>Once installed, to run it, just run&nbsp;<strong>mb</strong>:</p><p>You will be greeted with this if everything works:</p><p><ac:image ac:height="63"><ri:attachment ri:filename="image2018-11-14_16-53-23.png"></ri:attachment></ac:image></p><p><br></p></ac:layout-cell></ac:layout-section><ac:layout-section ac:type="single"><ac:layout-cell><p><br></p></ac:layout-cell></ac:layout-section><ac:layout-section ac:type="single"><ac:layout-cell><h2>Docker Setup:<ac:structured-macro ac:name="anchor" ac:schema-version="1" ac:macro-id="bc23ef32-6210-44f9-aa6a-12c318ac5386"><ac:parameter ac:name="">mb_docker</ac:parameter></ac:structured-macro></h2><h4>Pre-requisites:</h4><ul><li>Docker</li></ul><p><br></p><p>If you have docker installed on your machine you can simply run the following command in your terminal to get the latest mountebank container.</p><ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="5866a38a-63c1-417c-b136-5a6d113223dc"><ac:parameter ac:name="language">bash</ac:parameter><ac:plain-text-body><![CDATA[docker pull qldockerdtr.rockfin.com/qapow/mountebank
docker run mountebank]]></ac:plain-text-body></ac:structured-macro><p><br></p><p>If you would like to build your own docker image you can use the following docker file and build your own docker container for mountebank.</p><p>Copy the following code in a file and save it as <strong>Dockerfile</strong>:</p><ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="aafdc647-70d3-4525-9d45-c03ade105176"><ac:parameter ac:name="language">bash</ac:parameter><ac:plain-text-body><![CDATA[FROM alpine:3.8


EXPOSE 80
EXPOSE 2525

###
#Mountebank Stuffs
###
ADD ./imposters /mb

CMD ["mb", "--configfile", "/mb/imposters.ejs", "--allowInjection", "--loglevel=debug"]

ENV NODE_VERSION=8.11.4-r0

RUN apk update \
 && apk add --no-cache nodejs=${NODE_VERSION} \
 && apk add --no-cache npm=${NODE_VERSION}

ENV MOUNTEBANK_VERSION=1.15.0

RUN npm set unsafe-perm true \ 
 && npm install -g mountebank@${MOUNTEBANK_VERSION} --production \
 && npm cache clean --force 2>/dev/null \
 && rm -rf /tmp/npm*

]]></ac:plain-text-body></ac:structured-macro><p class="auto-cursor-target"><br></p><p>Run the following command in terminal to build and start the container</p><ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="8301ff8e-67a8-49c1-8b3f-6d1bf1afe947"><ac:parameter ac:name="language">bash</ac:parameter><ac:plain-text-body><![CDATA[docker build . -t mb
docker run -rm mb]]></ac:plain-text-body></ac:structured-macro><p class="auto-cursor-target"><br></p></ac:layout-cell></ac:layout-section></ac:layout>