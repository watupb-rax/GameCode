# GameCode
GameCode for chess

 //CODE FOR THE Game

  public class Game{
    private Player[] players;
    private Board board;
    private Player currentTurn;
    private GameStatus status;
    private Lst<Move> movesPlayed;

    private void initialize(PLayer p1, Player p2)
    {
      players[0] = p1;
      players[1] = p2;

      board.resetBoard();

      if(p1.isWhiteSide()){
        this.currentTurn = p1;
      }
      else{
        this.currentTurn = p2;
      }

      movesPlayed.clear();
    }

    public boolean isEnd()
    {
      return this.getStatus() != GameStatus.ACTIVE;
    }

    public boolean getStatus()
    {
      return this.status;
    }
    
    public void setStatus(GameStatus status)
  {
    this.status = status;
  }
  
  public boolean playerMove(Player player, int startX, int startY, int endX, int endY)
  
  {
  Spot startBox = board.getBox(startX, startY);
  Spot endBox = board.getBox(startY, endY);
  Move move = new Move(player, startBox, endBox);
  return this.makeMove(move, player);
  }
  
  private boolean makeMove(Move move, Player player)
  {
  Piece sourcePiece = move.getStart(). getPiece();
    if(sourcePiece == null){
     return false;
  }
    // valid player
    if (player != currentTurn){
        return false;
    }
    
    if (sourcePiece.isWhite() != player.isWhiteSide()) {
        return false;
      }
  
  //valid move
    if (!sourcePiece.canMove(board, move.getStart(), move.getEnd()))
  {
  return false;
  }
  
  //kill?
  Piece destPiece = move.getStart().getPiece();
  if (destPiece != null)
  {
  destPiece.setKilled(true);
  move.setPieceKilled(destPiece);
  }
  
  
  
        

  }
  
