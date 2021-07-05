FROM public.ecr.aws/lambda/python:3.8
COPY requirements.txt ./
RUN pip install --upgrade pip setuptools
RUN pip install -r requirements.txt

# Lambda function copy
COPY src ./src

# container Lambda で必要なhandler指定CMDは docker-compose または AWS Lambda の設定で上書きする