outdir ?= $(PWD)
.PHONY: srpm
srpm: selinux-policy
	dnf install -y rpkg
	cd selinux-policy && rpkg srpm --outdir . --spec selinux-policy.spec
	cp selinux-policy/*.src.rpm "$(outdir)"

selinux-policy:
	dnf install -y git rpmdevtools
	rm -rf selinux-policy
	git clone https://src.fedoraproject.org/rpms/selinux-policy.git -b f44 --depth 1
	sed -i \
		-e 's/^%global commit .*/%global commit main/' \
		-e 's/^Source: .*/Source: %{giturl}\/archive\/refs\/heads\/main.tar.gz/' \
		-e '/^%global shortcommit .*/d' \
		-e 's/^%global giturl .*/%global giturl https:\/\/github.com\/chlorodose\/selinux-policy/' \
		selinux-policy/selinux-policy.spec
	cd selinux-policy && spectool -g selinux-policy.spec
