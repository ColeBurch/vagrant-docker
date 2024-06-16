FROM python

RUN python3 -m pip install --upgrade pip

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . starter
WORKDIR /starter

ENTRYPOINT ["python3", "starter/manage.py"]
CMD ["runserver", "0.0.0.0:8000"]
