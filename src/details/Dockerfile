FROM ruby:3.3.0-slim

WORKDIR /opt/microservices

COPY ./Gemfile .
COPY ./details.rb .

RUN bundle install

ARG service_version
ARG enable_external_book_service
ENV SERVICE_VERSION=${service_version:-v1}
ENV ENABLE_EXTERNAL_BOOK_SERVICE=${enable_external_book_service:-false}

EXPOSE 9080

RUN useradd -u 1000 -m myuser
USER myuser

CMD ["ruby", "details.rb", "9080"]