FROM centos:7
LABEL \
    name="F2.0 Review Rot - Backend" \
    vendor="Factory 2.0 Team" \
    license="MIT"
RUN yum -y install git python-setuptools && yum -y clean all && \
    git clone https://github.com/nirzari/review-rot && \
    cd review-rot && \
    python setup.py install
USER 1001
ENTRYPOINT while true; do \
    review-rot -c /opt/configuration.yaml -f json --reverse > /opt/data/data-pending.json \
    && mv /opt/data/data-pending.json /opt/data/data.json \
    && sleep 600; \
done
