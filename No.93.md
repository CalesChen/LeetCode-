#DFS的初步使用
Attention1 ： 注意List类型中没有*Append* 方法

class Solution {
    static final int SEG_COUNT = 4;
    List<String> ans = new ArrayList<String>();
    int[] segments = new int[SEG_COUNT];

    public List<String> restoreIpAddresses(String s) {
        //segments = new int[SEG_COUNT];
        dfs(s,0,0);
        return ans;
    }
    public void dfs(String s, int segId, int segStart){
        if(segId == SEG_COUNT){
            if(segStart == s.length()){
                StringBuffer ipAddr = new StringBuffer();
                for(int i = 0; i<SEG_COUNT;i++){
                    ipAddr.append(segments[i]);
                    if( i != SEG_COUNT - 1){
                        ipAddr.append('.');
                    }
                }
                ans.add(ipAddr.toString());
            }
            return;
        }

        if(segStart == s.length()){
            return;
        }

        if(s.charAt(segStart) == '0'){
            segments[segId] = 0;
            dfs(s,segId+1, segStart+1);
        }

        int addr = 0;
        for(int segEnd = segStart;segEnd < s.length();segEnd ++){
            addr = addr * 10 + (s.charAt(segEnd) - '0');
            if(addr > 0 && addr <= 0xFF){
                segments[segId] = addr;
                dfs(s,segId+1,segEnd+1);  // Error: Segend mixed with SegStart
            }
            else{
                break;
            }
        }
    }
}
