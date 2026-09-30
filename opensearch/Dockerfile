ARG OPENSEARCH_VERSION
FROM docker.io/opensearchproject/opensearch:${OPENSEARCH_VERSION}
# Magento only uses core analysis. The bundled plugins, G1 and C2 roughly double idle memory.
RUN rm -rf plugins/* bin/opensearch-performance-analyzer \
    && sed -i '/performance-analyzer\|clk.tck\|allowAttachSelf\|jdk.attach/d' config/jvm.options \
    && printf '%s\n' -XX:-UseG1GC -XX:+UseSerialGC -XX:TieredStopAtLevel=1 > config/jvm.options.d/warden.options \
    && bin/opensearch-plugin install analysis-phonetic \
    && bin/opensearch-plugin install analysis-icu
