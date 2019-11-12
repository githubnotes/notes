https://github.west.isilon.com/isilon/onefs.git

pip install --trusted-host artifactory.west.isilon.com --index-url http://artifactory.west.isilon.com:8081/artifactory/api/pypi/pypi-repo/simple  isilon-ducttape-cli

dt --owner fzhou vcluster create --num-ips 4 BR_MASTER --location seattle
10.7.147.6

dt --owner arahimi vcluster create BR_MASTER --location sea1 --num-nodes 1

wget http://cribsbiox.west.isilon.com/home/cclayton/public/bug/bug254932/python2.7.core.gz
gdbcore `which python2.7` /root/python2.7.core.gz /mnt/bb/b.master.112/obj.RELEASE/symbols
 
make isi-isilon isi-isilon-install OVERRIDE=isilon/lib/isi_flexnet 
pkill isi_papi_d
isi network rules create groupnet0.subnet0.pool0.rule22 ext-1 --description 'practice rule 22'

/mnt/sharedfolder/onefs/isilon/lib/isi_flexnet
make checkcov
 lines......: 70.2% (5714 of 8143 lines)
functions..: 65.1% (549 of 843 functions)
 branches...: 54.5% (3598 of 6603 branches)

```cpp

TEST(conflicting_rules)
{
	struct isi_error *error = NULL;
	struct flx_rule rule_1 = {};
	int idx;

	for(idx = 0; idx < 1; idx++) {
		error = NULL;
		init_config(idx);

		/*
		 * Setup two bonding conflicted rules.
		 */
		flx_rule_clean(&rule_1);
	
		flx_rule_set_name(&rule_1, "rule_1");
		flx_rule_set_name(&rule_1, "rule_1");

		/*
		 * Try adding the rule 1 first and then the rule 1
		 */
		flx_pool_add_rule(pool, &rule_1, false, &error);
		fail_if_error(error);

		flx_pool_add_rule(pool, &rule_1, false, &error);
		fail_unless(error != null);

		flx_pool_remove_rule(pool, &rule_1, &error);
		fail_if_error(error);

		flx_pool_add_rule(pool, &rule_1, false, &error);
		fail_if_error(error);

		flx_rule_clean(&rule_1);
		
		if (config != NULL) {
			flx_config_free(config);
			config = NULL;
		}
	}
    
struct flx_rule {
	/**
	 * Increments when _dirty is set and config is saved
	 */
	uint64_t		 _revision;
	/**
	 * Name of rule
	 */
	char			*_name;
	/**
	 * Rule id
	 */
	uint32_t		_id;
	/**
	 * Name of description
	 */
	char			*_desc;
	/**
	 * Which node tpyes the rule applies to
	 */
	enum flx_node_filter	 _node_filter;
	/**
	 * What interfaces it applies to
	 */
	struct flx_iface_class	 _class;
	/**
	 * Is this a deprecated rule?
	 * Applies to rules targeting I Series filter rules are deprecated in 6.5.2.
	 */
	bool			 _deprecated;
	/**
	 * The parent pool. Lifetime owned by the parent pool (not the rule)
	 */
	struct flx_pool 	*_pool;
};

struct flx_pool {
	/**
	 * Provisioning rules: set of struct flx_rule
	 */
	struct flx_rule_set		_rules;

}



public int Helper(TreeNode root, int target){
	
	TreeNode up = null;
	TreeNode down = null;

	while(root != null){

		if(root.val > target){
			down = root;
			root = root.left;
		}else if(root.val < target){
			up = root;
			root = root.right;
		}else{

		}
	}

	if(Math.abs(up.val - target) > Math.abs(down.val - target)){
		return down.val;
	}

	return up.val;

}

```


REPRO:
* Test environment:
	Node types:
	Number of nodes: 1
	Clients:
	
* Test command(s) and/or Manual repro steps:
	isi network rules create groupnet0.subnet0.pool0.rule22 ext-1 --description 'practice rule 22
* Actual behavior:
	error message: rule22 duplicates rule0 on the same interface ext-1"
* Expected behavior
	error message: rule22 duplicates rule0 on the same interface ext-1"
* Test and/or save logs
	make isi-check OVERRIDE=isilon/lib/isi_flexnet. Total Passed 272. Total Failed: 0. Total Suite Erroes: 0
* In case of a panic, is node/cluster available for investigation? Please provide details

FACQS:
Frequency – 
	How many times have we seen this issue – in this branch: occasionally
	Is there an existing bug already tracking this? NO
Availability – Does or can this issue cause DU/DL? If yes, please explain how.
	No
Customer Impact – Would fixing this issue improve customer experience and/or avoid an escalation? If yes, please explain how.
	Yes. The error message will be clearer which will prevent confusion for the customer.
Quality – Does this fix improve product quality in some way? If yes, please explain how.
	Yes. Improve the product to more robust. If customers provide same rule, will provide clear error message to the engineer to fix the error.
Severity – What is the severity of the failure when it occurs?
	Sev3