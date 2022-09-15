FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8 AS build
WORKDIR /app
COPY requirements.txt .
RUN python -m pip install --upgrade pip && pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]