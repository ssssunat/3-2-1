# include <bits/stdc++.h>
  using namespace std;
  struct rope{
      long long key, prior, kol;
      rope *l, *r;
      rope(long long ke, long long pri = (rand()^rand())) : key(ke), prior(pri), kol(1), l(NULL), r(NULL) {}
  };
  typedef rope * node;
  
  long long get_tree_kol(node tree){
	  if(tree == NULL) return 0;
	  return (tree->kol);
  }
  
  void merge_t(node &t, node l, node r){
      if(l == NULL) t = r;
      else if(r == NULL) t = l;
      else if((l->prior) < (r->prior)){
        merge_t((r->l), l, (r->l));
        t = r;
        t->kol = get_tree_kol(t->l) + get_tree_kol(t->r) + 1;
      }
      else {
        merge_t((l->r), (l->r), r);
        t = l;
        t->kol = get_tree_kol(t->l) + get_tree_kol(t->r) + 1;
      }
  }
  
  void split_t(node t, int k, node &l, node &r){
      if(t == NULL) return void ( l = r = NULL );
      if((t->key) >= k){
        split_t((t->r), k, (t->r), r);
        l = t;
        if(l != NULL) l->kol = get_tree_kol(l->l) + get_tree_kol(l->r) + 1;
        if(r != NULL) r->kol = get_tree_kol(r->l) + get_tree_kol(r->r) + 1;
      }
      else {
        split_t((t->l), k, l, (t->l));
        r = t;
        if(l != NULL) l->kol = get_tree_kol(l->l) + get_tree_kol(l->r) + 1;
        if(r != NULL) r->kol = get_tree_kol(r->l) + get_tree_kol(r->r) + 1;
      }
  }
  
  int insert_t(node &t, node it){
      if(t == NULL){
		  t = it;
		  return 0;
	  }
      node A, C;
      split_t(t, (it->key), A, C);
      int ans = get_tree_kol(A);
      merge_t(t, A, it);
      merge_t(t, t, C);
      return ans;
  }
  
  void remove_t(node &t, long long x){
      if(t == NULL) return;
      node A, B, C;
      split_t(t, x, A, C);
      split_t(A, x + 1, A, B);
      merge_t(t, A, C);
  }

  long long get_key_by_id(node tree, int id){
	  if(tree == NULL) return -1;
	  if(id <= get_tree_kol(tree->l)) return get_key_by_id(tree->l, id);
	  id -= get_tree_kol(tree->l);
	  if(id == 1) return tree->key;
	  id--;
	  return get_key_by_id(tree->r, id);
  }

  int main(){
      srand( time(NULL) );
      long long n;
      cin >> n;
      node t = NULL;
      for(int i = 1; i <= n; i++){
        int a;
        cin >> a;
        if(a == 1){
            int x;
            cin >> x;
            cout << insert_t(t, new rope(x)) << '\n';
        }
        else {
			int y;
			cin >> y;
            y = y + 1;
			remove_t(t, get_key_by_id(t, y));
        }
      }
      return 0;
  }
