FROM deepbase/pytorch:1.8.1

COPY project/tvr/requirements.txt /tmp

RUN pip install --no-cache-dir -r /tmp/requirements.txt \
    && rm -f /tmp/requirements.txt \
    && CC="cc -mavx2" pip install --no-cache-dir -U --force-reinstall pillow-simd

WORKDIR "/code"