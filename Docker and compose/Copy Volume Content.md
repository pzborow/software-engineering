# Copy Volume Content

`docker volume create --name bosoby_dbdata_testing && docker run --rm -it -v bosoby_dbdata_staging:/from -v bosoby_dbdata_testing:/to alpine ash -c 'cd /from ; cp -av . /to'`