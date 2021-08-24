ARG KUBE_BUILD_IMAGE_CROSS_TAG=v1.16.7-1
ARG KUBE_BASE_IMAGE=k8s.gcr.io/build-image/kube-cross
ARG TARGETPLATFORM=linux/amd64

FROM ${KUBE_BASE_IMAGE}:${KUBE_BUILD_IMAGE_CROSS_TAG} as kube-builder
ENV KUBE_BUILD_PLATFORMS=${TARGETPLATFORM}
ENV HOME /go/src/k8s.io/kubernetes

WORKDIR ${HOME}
COPY . .
RUN make all WHAT=cmd/kubeadm GOFLAGS=-v GOGCFLAGS="-N -l" \

FROM scratch
COPY --from=kube-builder /go/src/k8s.io/kubernetes/_output/bin/kubeadm /kubeadm
