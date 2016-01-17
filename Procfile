web: uwsgi --ini=uwsgi.ini --http=0.0.0.0:$PORT -p1
worker_plus_beat: sentry --config=sentry.conf.py celery worker -c1 -B --loglevel=INFO
