all: push

TAG = latest
PREFIX = quay.io/jcmoraisjr/kube-loadbalancer
HAPROXY_IMAGE = contrib-haproxy

server: service_loadbalancer.go
	GOOS=linux godep go build -ldflags -w -v -o rootfs/service_loadbalancer ./service_loadbalancer.go ./loadbalancer_log.go

container: server
	docker build -t $(PREFIX):$(TAG) rootfs

push: container
	docker push $(PREFIX):$(TAG)

clean:
	# remove servicelb and contrib-haproxy images
	docker rmi -f $(HAPROXY_IMAGE):$(TAG) || true
	docker rmi -f $(PREFIX):$(TAG) || true
