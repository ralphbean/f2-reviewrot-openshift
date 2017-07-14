FROM nginx:alpine
LABEL \
    name="F2.0 Review Rot - Frontend" \
    vendor="Factory 2.0 Team" \
    license="MIT"
RUN yum -y install git && yum -y clean all
RUN git clone https://github.com/nirzari/review-rot && \
    ln -s $(pwd)/review-rot/web/* /usr/share/nginx/html/. && \
    rm /usr/share/nginx/html/js/default-data.json && \
    ln -s /opt/data/data.json /usr/share/nginx/html/js/default-data.json
