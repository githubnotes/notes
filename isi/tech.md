```cpp
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

```