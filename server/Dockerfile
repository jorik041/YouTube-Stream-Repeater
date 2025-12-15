# PRODUCTION DOCKERFILE
FROM python:3.13-slim

# install deps
COPY ./requirements.txt /tmp/requirements.txt
RUN pip3  --disable-pip-version-check --no-cache-dir install --break-system-packages -r /tmp/requirements.txt
RUN rm -v /tmp/requirements.txt
RUN pip3 install -U yt-dlp

RUN apt update && apt install -y ffmpeg libmagic-dev

# copy the source code
WORKDIR /home/user/app
COPY ./src ./

# fix ownership of stuff inside application folder
RUN chmod 555 -R .

# run uvicorn
CMD [ "python", "-m", "uvicorn", "server:app", "--host", "0.0.0.0", "--port", "4000", "--no-server-header", "--workers", "8" ]