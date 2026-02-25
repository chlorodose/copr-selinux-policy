outdir ?= $(PWD)
.PHONY: srpm
srpm: selinux-policy
	dnf install -y rpkg
	cd selinux-policy && TMPD=$$(mktemp -d) && \
	    rpkg srpm --outdir $${TMPD} --spec selinux-policy.spec && \
		cp $${TMPD}/*.src.rpm "$(outdir)"

selinux-policy:
	dnf install -y git find rpmdevtools
	rm -rf selinux-policy
	git clone https://src.fedoraproject.org/rpms/selinux-policy.git -b f44 --depth 1
	cd selinux-policy && git apply ../*.patch
	cd selinux-policy && spectool -g selinux-policy.spec
