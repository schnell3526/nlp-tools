FROM schnell3526/knp:debian as knp
FROM schnell3526/jumanpp:debian as jumanpp

FROM python:slim-buster

COPY --from=knp /usr/local/ /usr/local/
COPY --from=jumanpp /usr/local/bin/jumanpp /usr/local/bin/jumanpp
COPY --from=jumanpp /usr/local/libexec/jumanpp/ /usr/local/libexec/jumanpp/

RUN pip install pyknp

WORKDIR /work

CMD [ "python", "pyknp_test.py" ]